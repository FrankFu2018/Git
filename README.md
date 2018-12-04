# Git
路由表生成源代码
#include "pch.h"
#include <iostream>
#include"fstream"
using namespace std;
#define N 9
int COST[N + 1][N + 1];
int A[N + 1][N + 1];
int B[10][10];
void ReadData(const char* filename)
{
	ifstream fin;
	fin.open(filename);
	for (int i = 1; i <= N; i++)
		for (int j = 1; j <= N; j++)
			fin >> COST[i][j];
}
void ALL_PATHS()
{
	int i, j, k, m;
	for (i = 1; i <= N; i++)
		for (j = 1; j <= N; j++)
			A[i][j] = COST[i][j];
	for (i = 1; i <= N; i++)
		for (j = 1; j <= N; j++)
			for (k = 1; k <= N; k++)
				if (A[i][k] + A[k][j] < A[i][j])
				{
					A[i][j] = A[i][k] + A[k][j];
					B[i][j] = k;
                }
}
void main()
{
	int m;
	ReadData("data.txt");
	ALL_PATHS();
	cout << "输入想要查询的路由器的号码";
	cin >> m;
	cout << "****************路由器"<<m<<"的路由表***********************" << endl;
	cout << "-----目的主机所在网络---------------下一跳地址--------" << endl;
	for (int i = 1; i <= N; i++) {
		printf("       %d.x.x.x", i);
		if (B[m][i] == 0)B[m][i] = i;
		printf("                      路由器 %d号\n", B[m][i]);
     }
}

