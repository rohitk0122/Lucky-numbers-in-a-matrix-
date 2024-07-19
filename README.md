# Lucky-numbers-in-a-matrix-
class Solution {
    public List<Integer> luckyNumbers (int[][] matrix) {
        List<Integer> luckyNumbers = new ArrayList<>();

        // Step 1: Find the minimum element in each row
        int[] minRowElements = new int[matrix.length];
        for (int i = 0; i < matrix.length; i++) {
            int minElement = matrix[i][0];
            for (int j = 1; j < matrix[0].length; j++) {
                if (matrix[i][j] < minElement) {
                    minElement = matrix[i][j];
                }
            }
            minRowElements[i] = minElement;
        }

        // Step 2: Check if any of these minimum elements are the maximum in their respective columns
        for (int minElement : minRowElements) {
            boolean isLucky = true;
            int colIndex = -1;

            // Find the column index of the minElement
            for (int i = 0; i < matrix.length; i++) {
                for (int j = 0; j < matrix[0].length; j++) {
                    if (matrix[i][j] == minElement) {
                        colIndex = j;
                        break;
                    }
                }
                if (colIndex != -1) {
                    break;
                }
            }

            // Check if minElement is the maximum in its column
            for (int i = 0; i < matrix.length; i++) {
                if (matrix[i][colIndex] > minElement) {
                    isLucky = false;
                    break;
                }
            }

            if (isLucky) {
                luckyNumbers.add(minElement);
            }
        }

        return luckyNumbers;
    }
}
