#include<iostream>
#include<vector>
#include<string>
using namespace std;

class Terrorists
{
public:
	int requiredCost(vector<string> v)
	{
		result=500; prepare(v);
		for(int i=1;i<size;i++) 
		{
			for(;dfs(0,i);) for(int j=0;j<size;j++) visit[j]=false;
			result=min(result,tmp);
			prepare(v);
		}
		return result;
	}

private:
	int result,size,edge[50][50],tmp;
	bool visit[50];

	void prepare(vector<string> v)
	{
		size=v.size(); tmp=0;
		for(int i=0;i<size;i++) for(int j=0;j<size;j++) edge[i][j]=(v[i][j]-'0');
		for(int i=0;i<size;i++) visit[i]=0;
	}

	int dfs(int now,int target)
	{
		if(now==target) {tmp++; return 1;}
		if(visit[now]==true) return 0;

		visit[now]=true;
		for(int i=0;i<size;i++) if(edge[now][i]>0 && dfs(i,target))
		{
			edge[now][i]--;
			edge[i][now]++;
			return 1;
		}
		return 0;
	}
};
