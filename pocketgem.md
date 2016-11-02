# PocketGem

```java
import java.io.*;
import java.util.*;

public class PathFinder {
    public static void main(String[] args)
            throws FileNotFoundException, IOException {
        String filename = "input_1.txt";
        if (args.length > 0) {
        	filename = args[0];
        }
        
        List<String> answer = parseFile(filename);
        System.out.println(answer);
    }
    
    static List<String> parseFile(String filename)
    		throws FileNotFoundException, IOException {
    	/*
    	 *  Don't modify this function
    	 */
        BufferedReader input = new BufferedReader(new FileReader(filename));
        List<String> allLines = new ArrayList<String>();
        String line;
        while ((line = input.readLine()) != null) {
        	allLines.add(line);
        }
        input.close();

        return parseLines(allLines);    	
    }
    
    static List<String> parseLines(List<String> lines) {
    	Set<String> visited = new HashSet<String>();
    	Map<String, List<String>> graph = new HashMap<String, List<String>>();
    	List<String> res = new ArrayList<String>();
    	String[] ori_des = lines.get(0).split(" ");
    	String start = ori_des[0];
		String end = ori_des[1];
		for(int i = 1; i < lines.size(); i++) {
			String line = lines.get(i);
			String[] node = line.trim().split(":");
			List<String> list = Arrays.asList(node[1].trim().split(" "));
			graph.put(node[0].trim(), list);
		}
		traversal(start, end, "", visited, res, graph);
		return res;
    }
    
    private static void traversal(String start, String end, String path, Set<String> visited, List<String> res, Map<String, List<String>> graph) {
		String curPath = path;
		curPath += start;
		visited.add(start);
		if(start.equals(end)) {
			res.add(curPath);
		} else {
			List<String> adj = graph.get(start);
			if(adj != null) {
				for(String adjNode: adj) {
					if(!visited.contains(adjNode)) {
						traversal(adjNode, end, curPath, visited, res, graph);
					}
				}
			}
		}
		visited.remove(start);
	}
}



import java.io.*;
import java.text.*;
import java.util.*;

public class LogParser {
    public static void main(String[] args)
            throws FileNotFoundException, IOException {
        String filename = "./data/test1.txt";
        if (args.length > 0) {
        	filename = args[0];
        }

        String answer = parseFile(filename);
        System.out.println(answer);
    }

    static String parseFile(String filename)
            throws FileNotFoundException, IOException {
        /*
    	 *  Don't modify this function
    	 */
        BufferedReader input = new BufferedReader(new FileReader(filename));
        List<String> allLines = new ArrayList<String>();
        String line;
        while ((line = input.readLine()) != null) {
            allLines.add(line);
        }
        input.close();

        return parseLines(allLines.toArray(new String[allLines.size()]));
    }

    private static Date convertDate(String dateString) {
	    DateFormat df = new SimpleDateFormat("MM/dd/yyyy-hh:mm:ss");
	    Date date = new Date();
	    try {
	      date = df.parse(dateString);
	    } catch (ParseException ignored) {}
	    return date;
	}
    
    static String parseLines(String[] lines) {
    	Map<String, Integer> status = new HashMap<>();
    	status.put("START", 0);
        status.put("CONNECTED", 1);
        status.put("DISCONNECTED", -1);
        status.put("SHUTDOWN", -1);
        List<Date> times = new ArrayList<Date>();
        List<String> events = new ArrayList<String>();
        for (int i = 0; i < lines.length; i++) {
	        String[] line = lines[i].split(" :: ");
	        if(!status.containsKey(line[1])) {
	        	continue;
	        }
	        times.add(convertDate(line[0].substring(1, line[0].length()-1)));
	        events.add(line[1]);
        }
        long totalTime = times.get(times.size()-1).getTime() - times.get(0).getTime();
        long connectedTime = 0;
        long lastTimePoint = 0;
        for (int i=1; i<times.size(); i++) {
        	String currentEvent = events.get(i);
        	long currentTime = times.get(i).getTime();
        	if (status.get(currentEvent) > 0) {
        		lastTimePoint = currentTime;
        	} else if (lastTimePoint > 0) {
	            connectedTime += currentTime - lastTimePoint;
	            lastTimePoint = -1;
        	}
        }
        double ratio = (double) connectedTime / totalTime * 100;
        return String.format("%d%s", (int) ratio, "%");
    }
}

```