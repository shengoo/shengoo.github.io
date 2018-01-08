title: C#从文件byte[]获取文件mime（contentType）
link: http://www.sheng00.com/1002.html
author: admin
description: 
post_id: 1002
created: 2013/11/22 15:34:03
created_gmt: 2013/11/22 07:34:03
comment_status: open
post_name: c%e4%bb%8e%e6%96%87%e4%bb%b6byte%e8%8e%b7%e5%8f%96%e6%96%87%e4%bb%b6mime%ef%bc%88contenttype%ef%bc%89
status: publish
post_type: post

# C#从文件byte[]获取文件mime（contentType）

public class MimeHelper
        {
            public static int MimeSampleSize = 256;
    
            public static string DefaultMimeType = "application/octet-stream";
    
            [DllImport(@"urlmon.dll", CharSet = CharSet.Auto)]
            private extern static System.UInt32 FindMimeFromData(
                System.UInt32 pBC,
                [MarshalAs(UnmanagedType.LPStr)] System.String pwzUrl,
                [MarshalAs(UnmanagedType.LPArray)] byte[] pBuffer,
                System.UInt32 cbSize,
                [MarshalAs(UnmanagedType.LPStr)] System.String pwzMimeProposed,
                System.UInt32 dwMimeFlags,
                out System.UInt32 ppwzMimeOut,
                System.UInt32 dwReserverd
            );
    
    
            public static string GetMimeFromBytes(byte[] data)
            {
                try
                {
                    uint mimeType;
                    FindMimeFromData(0, null, data, (uint)MimeSampleSize, null, 0, out mimeType, 0);
    
                    var mimePointer = new IntPtr(mimeType);
                    var mime = Marshal.PtrToStringUni(mimePointer);
                    Marshal.FreeCoTaskMem(mimePointer);
    
                    return mime ?? DefaultMimeType;
                }
                catch
                {
                    return DefaultMimeType;
                }
            }
        }