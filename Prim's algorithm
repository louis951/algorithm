#include <iostream>
#include <vector>
#include<limits>
#include <iomanip>
using namespace std;
//#define Max_Weight INT_MAX
#define Max_Weight 101

struct Edge {
	int from, to;
	Edge() {};
	Edge(int u, int *v) :from(u), to(*v) {};
};

class GraphMST {
private:
	int V; //頂點
	vector<vector<int>> Graph;
	vector<struct Edge> edgesetMST;
public:
	GraphMST() :V(0) {};
	GraphMST(int n) :V(n) {
		Graph.resize(V);
		for (int i = 0; i < V; i++) {
			Graph[i].resize(V);
		}
	}
	void AddEdge(int from, int to, int weight);

	void PrintSortedGraph();
	void PrimMST(int Start);
	friend int MinKeyExtract(int *key, bool *visited, int size);
};

int MinKeyExtract(int *key, bool *visited, int size) {

	int min = Max_Weight, min_idx = 0;
	for (int i = 1; i < size; i++) {
		if (visited[i] == false && key[i] < min) {
			min = key[i];
			min_idx = i;
		}
	}
	return min_idx;
}

void GraphMST::PrintSortedGraph() {
	for (int i = 0; i < V - 2; i++) {
		if (edgesetMST[i].from > edgesetMST[i].to) {
			swap(edgesetMST[i].from, edgesetMST[i].to);
		}
		cout << edgesetMST[i].from << " " << edgesetMST[i].to << endl;
	}
}

void GraphMST::PrimMST(int Start) {

	int *key = new int[V];
	int *predecessor = new int[V];
	bool *visited = new bool[V];

	for (int i = 0; i < V; i++) {
		key[i] = Max_Weight;
		predecessor[i] = -1;
		visited[i] = false;//未拜訪
	}

	key[Start] = 0;
	for (int i = 1; i < V; i++) {
		int u = MinKeyExtract(key, visited, V);
		if (i != 1) {
			edgesetMST.push_back(Edge(u, &predecessor[u]));
		}
		visited[u] = true;
		for (int i = 1; i < V; i++) {
			if (visited[i] == false && Graph[u][i] != 0 && Graph[u][i] < key[i]) {
				predecessor[i] = u;
				key[i] = Graph[u][i];
			}
		}

	}
	PrintSortedGraph();
}

void GraphMST::AddEdge(int from, int to, int weight) {
	Graph[from][to] = weight;
	Graph[to][from] = weight;
}

int main() {
	int V, s, E;
	cin >> V >> E >> s;
	GraphMST G(++V);
	for (int i = 0; i < E; i++) {
		int u, v, w;
		cin >> u >> v >> w;
		G.AddEdge(u, v, w);
	}
	G.PrimMST(s);
}
