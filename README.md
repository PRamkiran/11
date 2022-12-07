1.Implement the data link layer framing methods such as character stuffing and bit stuffing
Program:
Character Stuffing:
import java.util.Scanner;
class Char
{
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		String in[]=new String[n];
		for (int i=0;i<n ;i++ ) 
		{
		        in[i]=sc.next();

		}
		for (int i=0;i<n ;i++ ) 
		{
		if(in[i].equals("dle"))
		{
			in[i]="deldle";
		}	
		}
		System.out.println("Transmitted Message :");
		System.out.print("dlestx");
		for (int i=0;i<n ;i++ ) 
		{
		     System.out.print(in[i]+" ");	
		}
		System.out.println("dletx");
	}
}
Bit Stuffing:
class BSC
{
	public static void BitStuffing(int N,int arr[])
	{
		int brr[]=new int[30];
		int i=0,j=0,k;
		int count =1;
		while(i<N)
		{
			if (arr[i]==1) {
				brr[j]=arr[i];
				for(k=i+1;k<N&&arr[k]==1&&count <5;k++)
				{
					j++;
					brr[j]=arr[i];
					count++;
					if(count==5)
					{
						j++;
						brr[j]=0;
					}
					else
					{
						brr[j]=arr[i];
					}
					j++;
					i++;
				}
				for (i=0;i<j ;i++ ) 
				{
				    System.out.println(brr[i]);	
				}
				
			}
		}
	}

	public static void main(String[] args) {
		int N=6;
		int arr[]={1,1,1,1,1,1};
		BitStuffing(N,arr);
	}
}
2.Write a C program to develop a DNS client server to resolve the given hostname.
3.Implement on a data set of characters the three CRC polynomials – CRC-12, CRC-16 and CRC-CCIP. 
#include<stdio.h>
#include<string.h>
#define N strlen(g)
char t[28],cs[28],g[28];
int a,e,c,b;
void xxor()
{
for(c=1;c<N;c++)
cs[c]=((cs[c]==g[c])?'0':'1');
}
void crc()
{
for(e=0;e<N;e++)
cs[e]=t[e];
do
{
if(cs[0]=='1')
xxor();
for(c=0;c<N-1;c++)
cs[c]=cs[c+1];
cs[c]=t[e++];
}while(e<=a+N-1);
}
int main()
{
int flag=0;
do{
printf("\n1.crc12\n2.crc16\n3.crc ccit\n4.exit\n\nEnter your option.");
scanf("%d",&b);
switch(b)
{
case 1:strcpy(g,"1100000001111");
break;
case 2:strcpy(g,"11000000000000101");
break;
case 3:strcpy(g,"10001000000100001");
break;
case 4:return 0;
}
printf("\n enter data:");
scanf("%s",t);
printf("\n-----------------------\n");
printf("\n generating polynomial:%s",g);
a=strlen(t);
for(e=a;e<a+N-1;e++)
t[e]='0';
printf("\n--------------------------\n");
printf("mod-ified data is:%s",t);
printf("\n-----------------------\n");
crc();
printf("checksum is:%s",cs);
for(e=a;e<a+N-1;e++)
t[e]=cs[e-a];
printf("\n-----------------------\n");
printf("\n final codeword is : %s",t);
printf("\n------------------------\n");
printf("\ntest error detection 0(yes) 1(no)?:");
scanf("%d",&e);
if(e==0)
{
do{
printf("\n\tenter the position where error is to be inserted:");
scanf("%d",&e);
}
while(e==0||e>a+N-1);
t[e-1]=(t[e-1]=='0')?'1':'0';
printf("\n-----------------------\n");
printf("\n\terroneous data:%s\n",t);
}
crc();
for(e=0;(e<N-1)&&(cs[e]!='1');e++);
if(e<N-1)
printf("error detected\n\n");
else
printf("\n no error detected \n\n");
printf("\n-----------------------");
}while(flag!=1);

crc();
for(e=0;(e<N-1)&&(cs[e]!='1');e++);
if(e<N-1)
printf("error detected\n\n");
else
printf("\n no error detected \n\n");
printf("\n-----------------------");
while(flag!=1);
}
4 Implement Dijkstra’s algorithm to compute the shortest path in a graph.
public class Dijkstra {

  public static void dijkstra(int[][] graph, int source) {
    int count = graph.length;
    boolean[] visitedVertex = new boolean[count];
    int[] distance = new int[count];
    for (int i = 0; i < count; i++) {
      visitedVertex[i] = false;
      distance[i] = Integer.MAX_VALUE;
    }
    distance[source] = 0;
    for (int i = 0; i < count; i++) {
      int u = findMinDistance(distance, visitedVertex);
      visitedVertex[u] = true;
      for (int v = 0; v < count; v++) {
        if (!visitedVertex[v] && graph[u][v] != 0 && (distance[u] + graph[u][v] < distance[v])) {
          distance[v] = distance[u] + graph[u][v];
        }
      }
    }
    for (int i = 0; i < distance.length; i++) {
      System.out.println(String.format("Distance from %s to %s is %s", source, i, distance[i]));
    }

  }
  private static int findMinDistance(int[] distance, boolean[] visitedVertex) {
    int minDistance = Integer.MAX_VALUE;
    int minDistanceVertex = -1;
    for (int i = 0; i < distance.length; i++) {
      if (!visitedVertex[i] && distance[i] < minDistance) {
        minDistance = distance[i];
        minDistanceVertex = i;
      }
    }
    return minDistanceVertex;
  }

  public static void main(String[] args) {
    int graph[][] = new int[][] { { 0, 0, 1, 2, 0, 0, 0 }, { 0, 0, 2, 0, 0, 3, 0 }, { 1, 2, 0, 1, 3, 0, 0 },
        { 2, 0, 1, 0, 0, 0, 1 }, { 0, 0, 3, 0, 0, 2, 0 }, { 0, 3, 0, 0, 2, 0, 1 }, { 0, 0, 0, 1, 0, 1, 0 } };
    Dijkstra T = new Dijkstra();
    T.dijkstra(graph, 0);
  }
}
Output:
5 Take an example subnet graph with weights indicating delay between nodes. Now obtain Routing table at each node using distance vector routing algorithm 
#include<stdio.h>
#include<conio.h>
struct node
{
    unsigned dist[20];
    unsigned from[20];
}rt[10];
int main()
{
    int costmat[20][20];
    int nodes,i,j,k,count=0;
    printf("\nEnter the number of nodes : ");
    scanf("%d",&nodes);
    printf("\nEnter the cost matrix :\n");
    for(i=0;i<nodes;i++)
    {
        for(j=0;j<nodes;j++)
        {
            scanf("%d",&costmat[i][j]);
            costmat[i][i]=0;
            rt[i].dist[j]=costmat[i][j];
            rt[i].from[j]=j;
        }
    }
        do
        {
            count=0;
            for(i=0;i<nodes;i++)
            for(j=0;j<nodes;j++)
            for(k=0;k<nodes;k++)
                if(rt[i].dist[j]>costmat[i][k]+rt[k].dist[j])
                {
                    rt[i].dist[j]=rt[i].dist[k]+rt[k].dist[j];
                    rt[i].from[j]=k;
                    count++;
                }
        }while(count!=0);
        for(i=0;i<nodes;i++)
        {
            printf("\n\n For router %d\n",i+1);
            for(j=0;j<nodes;j++)
            {
                printf("\t\nnode %d via %d Distance %d ",j+1,rt[i].from[j]+1,rt[i].dist[j]);
            }
        }
    printf("\n\n");
    getch();
}
6 Take an example subnet of hosts. Obtain broadcast tree for it. 
#include<stdio.h>

int a[10][10],n;

main()

{

int i,j,root;



printf("Enter no.of nodes:");

scanf("%d",&n);

printf("Enter adjacent matrix\n");

for(i=1;i<=n;i++)

for(j=1;j<=n;j++)

{

printf("Enter connecting of %d–>%d::",i,j);


scanf("%d",&a[i][j]);

}

printf("Enter root node:");

scanf("%d",&root);

adj(root);

}

adj(int k)

{

int i,j;

printf("Adjacent node of root node::\n");

printf("%d\n\n",k);

for(j=1;j<=n;j++)

{

if(a[k][j]==1 || a[j][k]==1)

printf("%d\t",j);

}

printf("\n");

for(i=1;i<=n;i++)

{

if((a[k][j]==0) && (a[i][k]==0) && (i!=k))

printf("%d",i);

}

}
7 Write a client-server application for chat using UDP 
Udp Client:
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.util.Scanner;

public class udpClient
{
	public static void main(String args[]) throws IOException
	{
		Scanner sc = new Scanner(System.in);
		DatagramSocket ds = new DatagramSocket();

		InetAddress ip = InetAddress.getLocalHost();
		byte buf[] = null;
		while (true)
		{
			String inp = sc.nextLine();
			buf = inp.getBytes();
			DatagramPacket DpSend =
				new DatagramPacket(buf, buf.length, ip, 1234);
			ds.send(DpSend);
			if (inp.equals("bye"))
				break;
		}
	}
}

Udp Server:
import java.io.IOException;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;
import java.net.SocketException;

public class udpServer
{
	public static void main(String[] args) throws IOException
	{
		DatagramSocket ds = new DatagramSocket(1234);
		byte[] receive = new byte[65535];

		DatagramPacket DpReceive = null;
		while (true)
		{
			DpReceive = new DatagramPacket(receive, receive.length);

			ds.receive(DpReceive);

			System.out.println("Client:-" + data(receive));
			if (data(receive).toString().equals("bye"))
			{
				System.out.println("Client sent bye.....EXITING");
				break;
			}

			receive = new byte[65535];
		}
	}
	public static StringBuilder data(byte[] a)
	{
		if (a == null)
			return null;
		StringBuilder ret = new StringBuilder();
		int i = 0;
		while (a[i] != 0)
		{
			ret.append((char) a[i]);
			i++;
		}
		return ret;
	}
}
8 Implement programs using raw sockets (like packet capturing and filtering)
#include<stdio.h>
#include<sys/types.h>
#include<errno.h>
#define SIZE 256
int main(){
	int srFd,CIFD,len;
	struct sockaddr_inserver,client;
	char buf[SIZE],buf1[SIZE];
	int n,j;
	FILE *fp,*fp1;
	srFd  = socket[AF_INET,Sock_STREAM,0];
	if(srFd<0){
		print("\n Socket Error");
		exit(0);
	}
	bzero[&server,sizeof[server]];
	server.sin_family = AF_INET;
	server.sin_port = htons[2200];
	server.sin_add.s_addr = htons[INADDRANY];
	if(bind[srFd,[struct sockadd *]&server,sizeof[server]] <0){
		printf("\n Server : binderror");
		close(srFd);
		exit(0);
	}
	if(listen(srFd,1)<0){
		printf("\n listen error");
		close(CIFD);
		exit(0);
	}
	printf("\n Server is ready to listen\n");
	len = sizeof(client);
	CIFD  = accept(srFd,(struct sockaddr*) &client,&len);
	if(CIFD<0){
		printf("\n Accept Error");
		close(CIFD);
		close(srFd);
		exit(0);
	}
	printf("Client gets connected\n");
	bzero(&buf,sizeof(buf));
	if((n=recv(CIFD,&buf,SIZE,0))<0){
		printf("\n Receive Error in Server \n");
		close(srFd);
		close(CIFD);
		exit(0);
	}
	buf[n-1] = NULL;
	printf("\n FILE Name %s",buf);
	if(n= send(CIFD,buf,strlen(buf,0))<0){
		printf("\n Error");
		close(CIFD);
		exit(0);
	}
	close(srFd);
	close(CIFD);
	exit(0);
}
 9 Write a C program to perform sliding window protocol. 
Program:
import java.io.*;
public class GoBackN {

 public static void main(String args[]) throws IOException
 {
  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
  
  System.out.println("Please enter the Window Size: ");
  int window = Integer.parseInt(br.readLine());
  
  boolean loop = true;
  int sent = 0;
  
  while(loop)
  {
   
   for(int i = 0; i < window; i++)
   {
    System.out.println("Frame " + sent + " has been transmitted.");
    sent++;
    if(sent == window)
     break;
   }
   
   System.out.println("Please enter the last Acknowledgement received.");
   int ack = Integer.parseInt(br.readLine());
   
   if(ack == window)
    loop = false;
   else
    sent = ack;
  }
  
 }
 
}
10 Get the MAC or Physical address of the system using Address Resolution Protocol. 
import java.net.InetAddress;
import java.net.NetworkInterface;
import java.net.SocketException;
import java.net.UnknownHostException;
import java.util.Scanner;

public class MacAddress {
    public static void main(String[] args)
    {
        try
        {
            Scanner console = new Scanner(System.in);
            System.out.println("Enter System Name: ");
            String ipaddr = console.nextLine();
            InetAddress address = InetAddress.getByName(ipaddr);
            System.out.println("address = "+address);
            NetworkInterface ni = NetworkInterface.getByInetAddress(address);
            if (ni!=null)
            {
                byte[] mac = ni.getHardwareAddress();
                if (mac != null)
                {
                    System.out.print("MAC Address : ");
                    for (int i=0; i < mac.length; i++)
                    {
                        System.out.format("%02X%s", mac[i], (i < mac.length - 1) ? "-" :"");
                    }
                }
                else
                {
                    System.out.println("Address doesn't exist or is not accessible/");
                    
                    }
                }
            else
            {
                System.out.println("Network Interface for the specified address is not found");
            }
        }
        catch(UnknownHostException | SocketException e)
        {
        }
    }    
}
11 Simulate the Implementing Routing Protocols using Border Gateway Protocol (BGP) 
1.	#include <stdio.h>
2.	#include<conio.h>
3.	int main()
4.	{
5.	int n;
6.	int i,j,k;
7.	int a[10][10],b[10][10];
8.	printf("\n Enter the number of nodes:");
9.	scanf("%d",&n);
10.	for(i=0;i<n;i++)
11.	{
12.	for(j=0;j<n;j++)
13.	{
14.	printf("\n Enter the distance between the host %d - %d:",i+1,j+1);
15.	scanf("%d",&a[i][j]);
16.	}}
17.	for(i=0;i<n;i++)
18.	{
19.	for(j=0;j<n;j++)
20.	{
21.	printf("%d\t",a[i][j]);
22.	}
23.	printf("\n");
24.	}
25.	for(k=0;k<n;k++)
26.	{
27.	for(i=0;i<n;i++)
28.	{
29.	for(j=0;j<n;j++)
30.	{
31.	if(a[i][j]>a[i][k]+a[k][j])
32.	{
33.	a[i][j]=a[i][k]+a[k][j];
34.	}}}}
35.	for(i=0;i<n;i++)
36.	{
37.	for(j=0;j<n;j++)
38.	{
39.	b[i][j]=a[i][j];
40.	if(i==j)
41.	{
42.	b[i][j]=0;
43.	}
44.	}}
45.	printf("\n The output matrix:\n");
46.	for(i=0;i<n;i++)
47.	{
48.	for(j=0;j<n;j++)
49.	{
50.	printf("%d\t",b[i][j]);
51.	}
52.	printf("\n");
53.	}
54.	getch();
55.	}
56.	 #include <stdio.h>
57.	#include<conio.h>
58.	int main()
59.	{
60.	int n;
61.	int i,j,k;
62.	int a[10][10],b[10][10];
63.	printf("\n Enter the number of nodes:");
64.	scanf("%d",&n);
65.	for(i=0;i<n;i++)
66.	{
67.	for(j=0;j<n;j++)
68.	{
69.	printf("\n Enter the distance between the host %d - %d:",i+1,j+1);
70.	scanf("%d",&a[i][j]);
71.	}}
72.	for(i=0;i<n;i++)
73.	{
74.	for(j=0;j<n;j++)
75.	{
76.	printf("%d\t",a[i][j]);
77.	}
78.	printf("\n");
79.	}
80.	for(k=0;k<n;k++)
81.	{
82.	for(i=0;i<n;i++)
83.	{
84.	for(j=0;j<n;j++)
85.	{
86.	if(a[i][j]>a[i][k]+a[k][j])
87.	{
88.	a[i][j]=a[i][k]+a[k][j];
89.	}}}}
90.	for(i=0;i<n;i++)
91.	{
92.	for(j=0;j<n;j++)
93.	{
94.	b[i][j]=a[i][j];
95.	if(i==j)
96.	{
97.	b[i][j]=0;
98.	}
99.	}}
100.	printf("\n The output matrix:\n");
101.	for(i=0;i<n;i++)
102.	{
103.	for(j=0;j<n;j++)
104.	{
105.	printf("%d\t",b[i][j]);
106.	}
107.	printf("\n");
108.	}
109.	getch();
110.	}
111.	 
112.	

12 Simulate the OPEN SHORTEST PATH FIRST routing protocol based on the cost assigned to the path.
#include <stdio.h>
#include <string.h>
int main()
{
int count,src_router,i,j,k,w,v,min;
int cost_matrix[100][100],dist[100],last[100];
int flag[100];
 printf("\n Enter the no of routers");
scanf("%d",&count); 
printf("\n Enter the cost matrix values:");
for(i=0;i<count;i++)
{
for(j=0;j<count;j++)
{
 printf("\n%d->%d:",i,j);
scanf("%d",&cost_matrix[i][j]);
if(cost_matrix[i][j]<0)cost_matrix[i][j]=1000;
}
}
 printf("\n Enter the source router:");
scanf("%d",&src_router);
for(v=0;v<count;v++)
{
flag[v]=0;
last[v]=src_router;
dist[v]=cost_matrix[src_router][v];
}
flag[src_router]=1;
for(i=0;i<count;i++)
{
min=1000;
for(w=0;w<count;w++)
{
if(!flag[w])
if(dist[w]<min)
{
v=w;
min=dist[w];
}
}
flag[v]=1;
for(w=0;w<count;w++)
{
if(!flag[w])
if(min+cost_matrix[v][w]<dist[w])
{
dist[w]=min+cost_matrix[v][w];
last[w]=v;
}
}
}
for(i=0;i<count;i++)
{
 printf("\n%d==>%d:Path taken:%d",src_router,i,i);
w=i;
while(w!=src_router)
{
 printf("\n<--%d",last[w]);w=last[w];
}
 printf("\n Shortest path cost:%d",dist[i]);
}
}
