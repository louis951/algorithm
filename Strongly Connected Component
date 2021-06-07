#include <iostream>
#include <list>
#include <stack>
#include <vector>
using namespace std;

class Graph{
	int V; 
	list<int> *adj;   
	void fillOrder(int v, bool visited[], stack<int> &Stack);
	void DFSUtil(int v, bool visited[], vector<int>&);
public:
	Graph(int V);
	void addEdge(int v, int w);
	void insertion_sort(vector<int>&);
	void printSCCs();
	Graph getTranspose();
};

Graph::Graph(int V){
	this->V = V;
	adj = new list<int>[V];
}

void Graph::DFSUtil(int v, bool visited[],vector<int>&CCS){
	visited[v] = true;
	CCS.push_back(v);

	list<int>::iterator i;
	for (i = adj[v].begin(); i != adj[v].end(); ++i)
		if (!visited[*i])
			DFSUtil(*i, visited,CCS);
}

Graph Graph::getTranspose(){
	Graph g(V);
	for (int v = 0; v < V; v++){
		list<int>::iterator i;
		for (i = adj[v].begin(); i != adj[v].end(); ++i)
		{
			g.adj[*i].push_back(v);
		}
	}
	return g;
}

void Graph::addEdge(int v, int w){
	adj[v].push_back(w); 
}

void Graph::fillOrder(int v, bool visited[], stack<int> &Stack){
	visited[v] = true;

	list<int>::iterator i;
	for (i = adj[v].begin(); i != adj[v].end(); ++i)
		if (!visited[*i])
			fillOrder(*i, visited, Stack);

	Stack.push(v);
}

void Graph::insertion_sort(vector<int>& A) {
	for (int i = 1; i < A.size(); i++) {
		int buffer = A[i];
		int j;
		for (j = i - 1; j >= 0 && A[j] > buffer; j--)
			A[j + 1] = A[j];
		A[j + 1] = buffer;
	}
}

void Graph::printSCCs(){
	stack<int> Stack;

	int *predecessor = new int[V];

	bool *visited = new bool[V];
	bool *visitedCCS = new bool[V];
	for (int i = 0; i < V; i++) {
		predecessor[i] = i;
		visited[i] = false;
		visitedCCS[i] = false;
	}
	visited[0] = true;
	visitedCCS[0] = true;

	for (int i = 0; i < V; i++)
		if (visited[i] == false)
			fillOrder(i, visited, Stack);

	Graph gr = getTranspose();

	for (int i = 0; i < V; i++)
		visited[i] = false;

	while (Stack.empty() == false){
		int v = Stack.top();
		Stack.pop();
		vector<int> CCS;
		if (visited[v] == false)
			gr.DFSUtil(v, visited, CCS);
		insertion_sort(CCS);
		CCS.push_back(0);
		for (int i = 0, j = 1; i < CCS.size() - 1; i++, j++) 
			predecessor[CCS[i]] = CCS[j];
		
	}
	for (int i = 0; i < V; i++) {
		int j;
		bool touch = false;
		for (j = i; j != 0; j = predecessor[j]) {
			if (visitedCCS[j] == false) {
				touch = true;
				cout << j << " ";
				visitedCCS[j] = true;
			}
		}
		if (touch) {
			cout << endl;
		}
	}
}

int main(){
	int V, E, s;
	cin >> V >> E >> s;
	Graph g(++V);
	for (int i = 0; i < E; i++) {
		int u, v;
		cin >> u >> v;
		g.addEdge(u, v);
	}
	g.printSCCs();
}
