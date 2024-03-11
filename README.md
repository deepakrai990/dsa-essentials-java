```Java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;

public class GraphRoadsAndLibraries {

    static ArrayList<ArrayList<Integer>> graph;
    static boolean[] visited;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int q = scanner.nextInt(); // Number of queries

        for (int i = 0; i < q; i++) {
            int n = scanner.nextInt(); // Number of cities (nodes)
            int m = scanner.nextInt(); // Number of roads (edges)
            long c_lib = scanner.nextLong(); // Cost to build a library
            long c_road = scanner.nextLong(); // Cost to build a road

            graph = new ArrayList<>();
            visited = new boolean[n + 1];

            for (int j = 0; j <= n; j++) {
                graph.add(new ArrayList<>());
            }

            // Read and build the graph
            for (int j = 0; j < m; j++) {
                int city1 = scanner.nextInt();
                int city2 = scanner.nextInt();
                graph.get(city1).add(city2);
                graph.get(city2).add(city1);
            }

            // Calculate and print the minimum cost
            long result = calculateMinimumCost(n, c_lib, c_road);
            System.out.println(result);
        }

        scanner.close();
    }

    static long calculateMinimumCost(int n, long c_lib, long c_road) {
        if (c_road >= c_lib || m == 0) {
            // It's cheaper to build a library in each city
            return n * c_lib;
        } else {
            // Use DFS or BFS to find connected components and calculate the cost
            long totalCost = 0;
            for (int i = 1; i <= n; i++) {
                if (!visited[i]) {
                    totalCost += c_lib + (dfs(i) - 1) * c_road;
                }
            }
            return totalCost;
        }
    }

    static int dfs(int node) {
        int count = 1;
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                count += dfs(neighbor);
            }
        }

        return count;
    }
}
```
