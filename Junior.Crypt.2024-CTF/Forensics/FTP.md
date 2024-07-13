## FTP

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/e67801e1-baa8-4697-bdf9-23c6a5b4bd3f)

## File forensics

* file: FTP_connection.dll

## Tool

* dnSpy

## Overview 

* FTP connection

## Solution

* open file source by dnSpy
* source code

```
using System;
using System.IO;
using System.Net;

// Token: 0x02000002 RID: 2
internal class a
{
	// Token: 0x06000003 RID: 3 RVA: 0x000020F4 File Offset: 0x000002F4
	private static void a()
	{
		string text = "127.0.0.1";
		string text2 = "user";
		string text3 = "12345_ftp_ctf";
		<Module>.i = 2081625616;
		string str = "ftp://";
		<Module>.l = -1592258590;
		<Module>.r = -1871252905;
		object a = null;
		<Module>.m = -1437277352;
		<Module>.a = a;
		<Module>.e = 1386028750;
		string str2 = text;
		string str3 = "/";
		<Module>.o = 2136656571;
		WebRequest webRequest = WebRequest.Create(str + str2 + str3);
		<Module>.q = -1852116043;
		<Module>.e = null;
		FtpWebRequest ftpWebRequest = (FtpWebRequest)webRequest;
		WebRequest webRequest2 = ftpWebRequest;
		int k = 1845842485;
		<Module>.l = -1410905245;
		<Module>.k = k;
		bool flag;
		<Module>.h = flag;
		string method = "NLST";
		<Module>.c = ftpWebRequest;
		webRequest2.Method = method;
		WebRequest webRequest3 = ftpWebRequest;
		string userName = text2;
		object b = null;
		<Module>.i = 1057425350;
		<Module>.b = b;
		ICredentials credentials = new NetworkCredential(userName, text3);
		<Module>.d = flag;
		<Module>.h = null;
		<Module>.i = 1308380089;
		<Module>.i = -1411494653;
		<Module>.d = "d8ae48e8-eddf-4ac1-92bb-a1ae04b6e56f9f88f09b-47f0-4d95-a0ef-da1c6232d9e25cbd4d20-b9c4-";
		<Module>.e = null;
		webRequest3.Credentials = credentials;
		int p = 1203310366;
		<Module>.k = 1657774894;
		<Module>.m = -1557401652;
		<Module>.p = p;
		<Module>.q = 744302617;
		FtpWebResponse ftpWebResponse = (FtpWebResponse)ftpWebRequest.GetResponse();
		Console.WriteLine("Directory List:");
		b.b = text;
		StreamReader streamReader = new StreamReader(ftpWebResponse.GetResponseStream());
		<Module>.o = -2051646939;
		StreamReader streamReader2 = streamReader;
		try
		{
			for (;;)
			{
				bool endOfStream = streamReader2.EndOfStream;
				int num = 0;
				<Module>.d = ftpWebRequest;
				bool flag2 = endOfStream == num;
				<Module>.e = null;
				flag = flag2;
				<Module>.o = -1978466511;
				<Module>.d = "1aa0ea33-b694-49ed-b660-fe8632bb1eeeb982e4ca-75cd-4";
				bool flag3 = flag;
				<Module>.f = 1957620381;
				int r = 2097519326;
				<Module>.n = -1932913121;
				<Module>.r = r;
				<Module>.a = null;
				if (!flag3)
				{
					break;
				}
				string value = streamReader2.ReadLine();
				<Module>.d = "c4e71e9a-6c6e-4c6d-b952-bf2c0c5ba3f231";
				<Module>.a = streamReader2;
				Console.WriteLine(value);
				<Module>.n = -1040838703;
				b.b = 1876936332;
			}
			<Module>.c = text3;
			object b2 = null;
			<Module>.q = -1950879357;
			<Module>.a = flag;
			b.b = b2;
			<Module>.i = 1503776956;
			<Module>.h = text;
		}
		finally
		{
			bool flag4 = streamReader2 != null;
			<Module>.h = null;
			object a2 = ftpWebRequest;
			<Module>.r = 1809257038;
			b.a = a2;
			b.b = 1952428595;
			<Module>.i = -563903361;
			<Module>.k = -1529522494;
			<Module>.f = 1818084011;
			if (flag4)
			{
				((IDisposable)streamReader2).Dispose();
			}
			<Module>.k = 1987339265;
		}
		WebResponse webResponse = ftpWebResponse;
		<Module>.a = null;
		webResponse.Close();
		object g = flag;
		int m = 796469985;
		int r2 = -1051365525;
		<Module>.p = 1335196033;
		<Module>.r = r2;
		<Module>.o = -1980982856;
		<Module>.m = m;
		<Module>.g = g;
		b.a = text3;
	}
}

```

* this code make ftp request to localhost to list all files in current directory

`ICredentials credentials = new NetworkCredential(userName, text3);`

* class NetworkCredential(string userName, string password)

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/20fd8f51-c82b-447a-86a6-41f7a7d9306a)

* FTP password is initialize in `text3` variable

`string text3 = "12345_ftp_ctf";`

`grodno{12345_ftp_ctf}`


