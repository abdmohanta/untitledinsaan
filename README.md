# untitledinsaan




package com.debasish.arraypractice.oneDimensionalArray;

import java.util.LinkedList;
import java.util.Queue;

public class OneDimensionalArray97 {

    public static void main(String[] args) {

        // ======================================
        // PROBLEM 98: SHORTEST PATH IN BINARY MATRIX
        // ======================================

        // Step 1: create grid
        int[][] grid = {
                {0, 1},
                {1, 0}
        };

        int n = grid.length;

        // Step 2: check blocked cells
        if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1) {

            System.out.println("No Path");
            return;
        }

        // Step 3: directions (8 directions)
        int[] rowDir = {-1, -1, -1, 0, 0, 1, 1, 1};
        int[] colDir = {-1, 0, 1, -1, 1, -1, 0, 1};

        // queue -> row, col, distance
        Queue<int[]> queue = new LinkedList<>();

        queue.offer(new int[]{0, 0, 1});

        // mark visited
        grid[0][0] = 1;

        int shortest = -1;

        // Step 4: BFS traversal
        while (!queue.isEmpty()) {

            int[] current = queue.poll();

            int row = current[0];
            int col = current[1];
            int distance = current[2];

            // reached destination
            if (row == n - 1 && col == n - 1) {

                shortest = distance;
                break;
            }

            // explore neighbors
            for (int i = 0; i < 8; i++) {

                int newRow = row + rowDir[i];
                int newCol = col + colDir[i];

                // valid cell
                if (newRow >= 0 && newCol >= 0
                        && newRow < n && newCol < n
                        && grid[newRow][newCol] == 0) {

                    queue.offer(new int[]{
                            newRow,
                            newCol,
                            distance + 1
                    });

                    // mark visited
                    grid[newRow][newCol] = 1;
                }
            }
        }

        // Step 5: print result
        System.out.println("Shortest Path Length: " + shortest);

    }
}
