#include <limits.h>
#include <iostream>
#include <vector>
#include <stdio.h>
using namespace std;

#define INFIN 10000000
int vertex, edge, root;
vector<vector<int>> route;
vector<int> EdgeCost;


int minDistance(int dist[], bool sptSet[])
{
	int min = INFIN, min_index;

	for (int v = 0; v < vertex; v++)
		if (sptSet[v] == false && dist[v] <= min)
			min = dist[v], min_index = v;

	return min_index;
}


void dijkstra(vector<vector<int>> &graph, int src)
{
	int *dist = new int [vertex]; 
	bool *sptSet = new bool[vertex]; 

	for (int i = 0; i < vertex; i++)
		dist[i] = INFIN, sptSet[i] = false;

	dist[src] = 0;

	for (int count = 0; count < vertex - 1; count++) {
		int u = minDistance(dist, sptSet);

		sptSet[u] = true;

		for (int v = 0; v < vertex; v++)

			if (!sptSet[v] && graph[u][v] && dist[u] != INFIN && dist[u] + graph[u][v] < dist[v])
			{
				dist[v] = dist[u] + graph[u][v];
				EdgeCost[v] = graph[u][v];
			}
	}
}

void init()
{
	route = vector<vector<int>>(vertex, vector<int>(vertex));
	EdgeCost = vector<int>(vertex);
	for (int i = 0; i < vertex; i++)
		EdgeCost[i] = 0;
	for (int i = 0; i < vertex; i++)
		for (int j = 0; j < vertex; j++)
			route[i][j] = 0;
}

void readData()
{
	cin >> vertex >> edge;
	cin >> root;
	root -= 1;
	init();
	for (int i = 0; i < edge; i++)
	{
		int from, to, weight;
		cin >> from >> to >> weight;
		route[from - 1][to - 1] = weight;
	}
}

int main()
{
	
	readData();
	dijkstra(route, root);

	int total = 0;
	for (auto i : EdgeCost) total += i;
	cout << total;
	return 0;
}
