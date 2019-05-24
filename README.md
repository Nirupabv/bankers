# bankers
import java.util.*;
public class banker
{

	 static void safety(int a[][],int m[][],int w[],int r,int pn,int n[][])
	{
		int f[]=new int[pn];
		for(int i=0;i<pn;i++)
			f[i]=0;
		int o[]=new int[pn];
		int c=0;
		for(int j=0;j<pn;j++)
		{
			for(int i=0;i<pn;i++)
			{
				if(f[i]==0)
				{
					int flag=0;
					for(int k=0;k<r;k++)
					{
						if(n[i][k]<=w[k])
							flag=1;
						else
						{
							flag=0;
							break;
						}
					}
					if(flag==1)
					{
						for(int k=0;k<r;k++)
							w[k]=w[k]+a[i][k];
						f[i]=1;
						o[c]=i;
						c++;
					}
				}
			}
		}
		System.out.println("safe sequence is");
		for(int i=0;i<pn;i++)
			System.out.print(o[i]+"-->");
	}
	public static void main(String args[])
	{
		Scanner sc=new Scanner(System.in);
		System.out.println("enter no of processes and resources");
		int pn=sc.nextInt();
		int re=sc.nextInt();
		int a[][]=new int[pn][re];
		int m[][]=new int[pn][re];
		int n[][]=new int[pn][re];
		int w[]=new int[re];
		System.out.println("enter allocation");
		for (int i=0;i<pn;i++)
			for (int j=0;j<re;j++)
				a[i][j]=sc.nextInt();
		System.out.println("enter max");
		for (int i=0;i<pn;i++)
			for (int j=0;j<re;j++)
			{	m[i][j]=sc.nextInt();
				n[i][j]=m[i][j]-a[i][j];
			}
		System.out.println("enter available");
		for (int i=0;i<re;i++)
			w[i]=sc.nextInt();
		System.out.println("1.resource request 2.safe sequence");
		int x=sc.nextInt();
		if (x==1)
		{
			System.out.println("enter process no. and resouce request");
			int z=sc.nextInt();
			int rr[]=new int[re];
			for(int i=0;i<re;i++)
				rr[i]=sc.nextInt();
			int flag=0;
			for(int i=0;i<re;i++)
			{
				if(rr[i]<=n[z][i] && rr[i]<=w[i])
					flag=1;
				else 
				{
					flag=0;
					break;
				}
			}
			if(flag==1)
			{
				for(int i=0;i<re;i++)
				{
					w[i]-=rr[i];
					a[z][i]+=rr[i];
					n[z][i]-=rr[i];
				}
			}
		}
		safety(a,m,w,re,pn,n);
	}
	
}
