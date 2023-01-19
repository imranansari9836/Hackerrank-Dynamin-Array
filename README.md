class Result {

  

     public static List<Integer> dynamicArray(int n, List<List<Integer>> queries) {
        int lastAnswer = 0;
        List<Integer> answers = new ArrayList<Integer>();
        List<List<Integer>> arr = new ArrayList<List<Integer>>(n);
        for (int i = 0; i < n; i++) {
            arr.add(new ArrayList<Integer>());
        }
        
        for (List<Integer> query : queries) {
            final int queryType = query.get(0);
            final int x = query.get(1);
            final int y = query.get(2);
            int idx;
            if (queryType == 1) {
                idx = ((x ^ lastAnswer) % n);
                arr.get(idx).add(y);
            } else {
                idx = ((x ^ lastAnswer) % n);
                final int size = arr.get(idx).size();
                lastAnswer = arr.get(idx).get(y % size);
                answers.add(lastAnswer);
            }
        }

        return answers;
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int q = Integer.parseInt(firstMultipleInput[1]);

        List<List<Integer>> queries = new ArrayList<>();

        for (int i = 0; i < q; i++) {
            String[] queriesRowTempItems = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

            List<Integer> queriesRowItems = new ArrayList<>();

            for (int j = 0; j < 3; j++) {
                int queriesItem = Integer.parseInt(queriesRowTempItems[j]);
                queriesRowItems.add(queriesItem);
            }

            queries.add(queriesRowItems);
        }

        List<Integer> result = Result.dynamicArray(n, queries);

        for (int i = 0; i < result.size(); i++) {
            bufferedWriter.write(String.valueOf(result.get(i)));

            if (i != result.size() - 1) {
                bufferedWriter.write("\n");
            }
        }

        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
