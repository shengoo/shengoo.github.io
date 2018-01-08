title: 深入浅出单实例Singleton设计模式
link: http://www.sheng00.com/366.html
author: admin
description: 
post_id: 366
created: 2012/03/31 13:06:50
created_gmt: 2012/03/31 05:06:50
comment_status: open
post_name: %e6%b7%b1%e5%85%a5%e6%b5%85%e5%87%ba%e5%8d%95%e5%ae%9e%e4%be%8bsingleton%e8%ae%be%e8%ae%a1%e6%a8%a1%e5%bc%8f
status: publish
post_type: post

# 深入浅出单实例Singleton设计模式

长时间没有用java单实例模式，现在想起来有点忘了，发些东西大家一起熟悉下。 单实例Singleton设计模式可能是被讨论和使用的最广泛的一个设计模式了，这可能也是面试中问得最多的一个设计模式了。这个设计模式主要目的是想在整个系统中只能出现一个类的实例。这样做当然是有必然的，比如你的软件的全局配置信息，或者是一个Factory，或是一个主控类，等等。你希望这个类在整个系统中只能出现一个实例。当然，作为一个技术负责人的你，你当然有权利通过使用非技术的手段来达到你的目的。比如：你在团队内部明文规定，“XX类只能有一个全局实例，如果某人使用两次以上，那么该人将被处于2000元的罚款！”（呵呵），你当然有权这么做。但是如果你的设计的是东西是一个类库，或是一个需要提供给用户使用的API，恐怕你的这项规定将会失效。因为，你无权要求别人会那么做。所以，这就是为什么，我们希望通过使用技术的手段来达成这样一个目的的原因。 本文会带着你深入整个Singleton的世界，当然，我会放弃使用C++语言而改用Java语言，因为使用Java这个语言可能更容易让我说明一些事情。 Singleton的教学版本 这里，我将直接给出一个Singleton的简单实现，因为我相信你已经有这方面的一些基础了。我们姑且把这具版本叫做1.0版 
    
    
    // version 1.0    
    public class Singleton    
    {    
        private static final Singleton singleton = null;    
        private Singleton()    {    }    
    
        public static Singleton getInstance()    
        {    
            if (singleton == null)    
            {    
                singleton = new Singleton();    
            }    
            return singleton;    
        }    
    }

在上面的实例中，我想说明下面几个Singleton的特点：（下面这些东西可能是尽人皆知的，没有什么新鲜的） 1\. 私有（private）的构造函数，表明这个类是不可能形成实例了。这主要是怕这个类会有多个实例。 2\. 即然这个类是不可能形成实例，那么，我们需要一个静态的方式让其形成实例：getInstance()。注意这个方法是在new自己，因为其可以访问私有的构造函数，所以他是可以保证实例被创建出来的。 3\. 在getInstance()中，先做判断是否已形成实例，如果已形成则直接返回，否则创建实例。 4\. 所形成的实例保存在自己类中的私有成员中。 5\. 我们取实例时，只需要使用Singleton.getInstance()就行了。 当然，如果你觉得知道了上面这些事情后就学成了，那我给你当头棒喝一下了，事情远远没有那么简单。 Singleton的实际版本 上面的这个程序存在比较严重的问题，因为是全局性的实例，所以，在多线程情况下，所有的全局共享的东西都会变得非常的危险，这个也一样，在多线程情况下，如果多个线程同时调用getInstance()的话，那么，可能会有多个进程同时通过 (singleton== null)的条件检查，于是，多个实例就创建出来，并且很可能造成内存泄露问题。嗯，熟悉多线程的你一定会说——“我们需要线程互斥或同步”，没错，我们需要这个事情，于是我们的Singleton升级成1.1版，如下所示： 
    
    
    // version 1.1
    public class Singleton
    {
        private static final Singleton singleton = null;
        private Singleton()
        {
        }
    
        public static Singleton getInstance()
        {
            if (singleton == null)
            {
                synchronized (Singleton.class) 
                {
                    singleton = new Singleton();
                }
            }
            return singleton;
        }
    }

嗯，使用了Java的synchronized方法，看起来不错哦。应该没有问题了吧？！错！这还是有问题！为什么呢？前面已经说过，如果有多个线程同时通过(singleton== null)的条件检查（因为他们并行运行），虽然我们的synchronized方法会帮助我们同步所有的线程，让我们并行线程变成串行的一个一个去 new，那不还是一样的吗？同样会出现很多实例。嗯，确实如此！看来，还得把那个判断(singleton== null)条件也同步起来。于是，我们的Singleton再次升级成1.2版本，如下所示： 
    
    
    // version 1.2
    public class Singleton
    {
        private static final Singleton singleton = null;
        private Singleton()
        {
        }
    
        public static Singleton getInstance()
        {
            synchronized (Singleton.class)
            {
                if (singleton == null)
                {
                    singleton = new Singleton();
                }
            }
            return singleton;
        }
    }

不错不错，看似很不错了。在多线程下应该没有什么问题了，不是吗？的确是这样的，1.2版的Singleton在多线程下的确没有问题了，因为我们同步了所有的线程。只不过嘛……，什么？！还不行？！是的，还是有点小问题，我们本来只是想让new这个操作并行就可以了，现在，只要是进入 getInstance()的线程都得同步啊，注意，创建对象的动作只有一次，后面的动作全是读取那个成员变量，这些读取的动作不需要线程同步啊。这样的作法感觉非常极端啊，为了一个初始化的创建动作，居然让我们达上了所有的读操作，严重影响后续的性能啊！ 还得改！嗯，看来，在线程同步前还得加一个(singleton== null)的条件判断，如果对象已经创建了，那么就不需要线程的同步了。OK，下面是1.3版的Singleton。 
    
    
    // version 1.3
    public class Singleton
    {
        private static final Singleton singleton = null;
        private Singleton()
        {
        }
    
        public static Singleton getInstance()
        {
            if (singleton == null)
            {
                synchronized (Singleton.class)
                {
                    if (singleton == null)
                    {
                        singleton = new Singleton();
                    }
                }
            }
            return singleton;
        }
    }

感觉代码开始变得有点罗嗦和复杂了，不过，这可能是最不错的一个版本了，这个版本又叫“双重检查”Double-Check。下面是说明： 1\. 第一个条件是说，如果实例创建了，那就不需要同步了，直接返回就好了。 2\. 不然，我们就开始同步线程。 3\. 第二个条件是说，如果被同步的线程中，有一个线程创建了对象，那么别的线程就不用再创建了。 相当不错啊，干得非常漂亮！请大家为我们的1.3版起立鼓掌！