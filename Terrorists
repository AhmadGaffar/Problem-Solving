#include<iostream>
#include<vector>
#include<string>
#include<algorithm>
using namespace std;

vector<int> result;
int numNode,numServ,serv[41][11],step;
bool v[41][11][41],visit[41][1000],flag;
struct prob{int name; vector<short> serv;};
struct edge{prob a,b; int cost;};
vector<edge> on;

class IslandFerries
{
public:
	vector<int> costs(vector<string> legs,vector<string> prices)
	{
		prepare(legs,prices);
		bfs();
		return result;
	}

private:
	void prepare(vector<string> legs,vector<string> prices)
	{
		numNode=prices.size();
		numServ=legs.size();
		for(int i=0;i<numNode;i++) inServs(prices[i],i+1);
		for(int i=0;i<numServ;i++) inLegs(legs[i],i+1);
		for(int i=2;i<=numNode;i++) result.push_back(-1);
	}

	void inServs(string s,int index)
	{
		int x=0,num=1; s+=' ';
		for(int i=0;i<s.size();i++)
		{
			if(s[i]==' ') {serv[index][num]=x; x=0; num++; continue;}
			else x=(x*10)+(s[i]-'0');
		}
	}

	void inLegs(string s,int index)
	{
		int x=0,y=0,dash=0; s+=' ';
		for(int i=0;i<s.size();i++)
		{
			if(s[i]=='-') {dash=1; continue;}
			if(s[i]==' ') {x++; y++; v[x][index][y]=true; x=y=dash=0; continue;}

			if(dash==0) x=(x*10)+(s[i]-'0');
			else        y=(y*10)+(s[i]-'0');
		}
	}

	void bfs()
	{
		vector<short> tmp; in(1,tmp);
		for(step=1;on.size() && step<44000;step++)
		{
			for(int i=0;i<on.size();i++) on[i].cost--;
			for(int i=0;i<on.size();i++) if(on[i].cost==0) in(on[i].b.name,on[i].b.serv);
			for(int i=0;i<on.size();i++) if(visit[on[i].b.name][own(on[i].b.serv)]==true) {on.erase(on.begin()+i); i--;}
		}
	}

	void in(int name,vector<short> ticket)
	{
		if(ticket.size()==0 && visit[name][0]==false && name>=2) result[name-2]=step;

		visit[name][own(ticket)]=true;

		for(int j=0;j<ticket.size();j++) for(int k=1;k<=numNode;k++) if(v[name][ticket[j]][k]==true)// buy zero ticket
		{
			vector<short> S;
			for(int s=0;s<ticket.size();s++) if(ticket[s]!=ticket[j]) S.push_back(ticket[s]);
			if(visit[k][own(S)]==false) in(k,S);
		}
		if(ticket.size()<=2) for(int i=1;i<=numServ;i++)//buy one ticket
		{
			flag=true;
			for(int j=0;j<ticket.size();j++) if(ticket[j]==i) flag=false;
			if(flag==true) 
			{
				edge e;
				e.a.name=name;
				e.b.name=name;
				e.b.serv=ticket;
				e.b.serv.push_back(i); sort(e.b.serv.begin(),e.b.serv.end());
				e.cost=serv[name][i];
				if(visit[name][own(e.b.serv)]==false) on.push_back(e);
			}
		}
		if(ticket.size()<=1) for(int i=1;i<=numServ;i++) for(int i2=i+1;i2<=numServ;i2++) //buy two ticket
		{
			flag=true;
			for(int j=0;j<ticket.size();j++) if(ticket[j]==i || ticket[j]==i2) flag=false;
			if(flag==true) 
			{
				edge e;
				e.a.name=name;
				e.b.name=name;
				e.b.serv=ticket;
				e.b.serv.push_back(i); e.b.serv.push_back(i2); sort(e.b.serv.begin(),e.b.serv.end());
				e.cost=serv[name][i]+serv[name][i2];
				if(visit[name][own(e.b.serv)]==false) on.push_back(e);
			}
		}
		if(ticket.size()==0) for(int i=1;i<=numServ;i++) for(int i2=i+1;i2<=numServ;i2++) for(int i3=i2+1;i3<=numServ;i3++) //buy three ticket
		{
			edge e;
			e.a.name=name;
			e.b.name=name;
			e.b.serv=ticket;
			e.b.serv.push_back(i); e.b.serv.push_back(i2); e.b.serv.push_back(i3);
			e.cost=serv[name][i]+serv[name][i2]+serv[name][i3];
			if(visit[name][own(e.b.serv)]==false) on.push_back(e);
		}
	}

	inline short own(vector<short> x)
	{
		int ret=0;
		for(int i=0;i<x.size();i++) ret=ret*10+x[i];
		return ret;
	}
};
