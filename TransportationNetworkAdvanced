import java.awt.*;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;

public class TransportationNetworkAdvanced extends JFrame {

    private Map<String, Point> cityPositions;
    private Map<String, Map<String, Integer>> graph;

    private JTextArea outputArea;
    private GraphPanel graphPanel;

    private String sourceCity;

    private int cityCounter;

    private String mode;

    private Set<String> reachableCities;
    private Set<String> mstEdges;
    private Set<String> shortestPathEdges;

    public TransportationNetworkAdvanced() {

        cityPositions = new HashMap<>();
        graph = new HashMap<>();

        reachableCities = new HashSet<>();
        mstEdges = new HashSet<>();
        shortestPathEdges = new HashSet<>();

        cityCounter = 1;
        mode = "CITY";

        setTitle("Transportation Network Advanced");
        setSize(1200, 750);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        JPanel topPanel = new JPanel();

        JButton addCityBtn =
                new JButton("Add City");

        JButton addRoadBtn =
                new JButton("Add Road");

        JButton setSourceBtn =
                new JButton("Set Source");

        JButton bfsBtn =
                new JButton("BFS");

        JButton dijkstraBtn =
                new JButton("Dijkstra");

        JButton mstBtn =
                new JButton("Prim MST");

        JButton reachabilityBtn =
                new JButton("Reachability");

        JButton clearBtn =
                new JButton("Clear Output");

        topPanel.add(addCityBtn);
        topPanel.add(addRoadBtn);
        topPanel.add(setSourceBtn);
        topPanel.add(bfsBtn);
        topPanel.add(dijkstraBtn);
        topPanel.add(mstBtn);
        topPanel.add(reachabilityBtn);
        topPanel.add(clearBtn);

        add(topPanel, BorderLayout.NORTH);

        outputArea = new JTextArea();

        outputArea.setEditable(false);

        JScrollPane scrollPane =
                new JScrollPane(outputArea);

        scrollPane.setPreferredSize(
                new Dimension(300, 0));

        add(scrollPane, BorderLayout.EAST);

        graphPanel = new GraphPanel();

        add(graphPanel, BorderLayout.CENTER);

        addCityBtn.addActionListener(e -> {
            mode = "CITY";
        });

        addRoadBtn.addActionListener(e -> {
            mode = "ROAD";
        });

        setSourceBtn.addActionListener(e -> {

            String city =
                    JOptionPane.showInputDialog(
                            this,
                            "Enter Source City");

            if(city != null &&
                    graph.containsKey(city)) {

                sourceCity = city;

                graphPanel.repaint();
            }
        });

        bfsBtn.addActionListener(
                e -> runBFS());

        dijkstraBtn.addActionListener(
                e -> runDijkstra());

        mstBtn.addActionListener(
                e -> runMST());

        reachabilityBtn.addActionListener(
                e -> runReachability());

        clearBtn.addActionListener(e -> {
            outputArea.setText("");
        });

        setVisible(true);
    }

    class GraphPanel extends JPanel {

        private String firstCity;

        public GraphPanel() {

            setBackground(Color.WHITE);

            addMouseListener(
                    new MouseAdapter() {

                public void mouseClicked(
                        MouseEvent e) {

                   if(mode.equals("CITY")) {

    String cityName =
            JOptionPane.showInputDialog(
                    null,
                    "Enter City Name");

    if(cityName == null ||
       cityName.trim().isEmpty())
        return;

    cityPositions.put(
            cityName,
            new Point(
                    e.getX(),
                    e.getY()));

    graph.put(
            cityName,
            new HashMap<>());

    repaint();
}

                    else if(mode.equals("ROAD")) {

                        String city =
                                getCityAt(
                                        e.getX(),
                                        e.getY());

                        if(city == null)
                            return;

                       if(firstCity == null) {

    firstCity = city;

    JOptionPane.showMessageDialog(
            null,
            "Selected First City: " + city);
}

else {

    if(firstCity.equals(city)) {

        JOptionPane.showMessageDialog(
                null,
                "Cannot connect a city to itself!");

        firstCity = null;
        return;
    }

    if(graph.get(firstCity).containsKey(city)) {

        JOptionPane.showMessageDialog(
                null,
                "Road already exists!");

        firstCity = null;
        return;
    }

    String distStr =
            JOptionPane.showInputDialog(
                    "Enter Distance");
                            try {

                                int distance =
                                        Integer.parseInt(
                                                distStr);

                                graph.get(firstCity)
                                        .put(
                                                city,
                                                distance);

                                graph.get(city)
                                        .put(
                                                firstCity,
                                                distance);

                            }

                            catch(Exception ex) {

                                JOptionPane.showMessageDialog(
                                        null,
                                        "Invalid Distance");
                            }

                            firstCity = null;

                            repaint();
                        }
                    }
                }
            });
        }
                @Override
        protected void paintComponent(
                Graphics g) {

            super.paintComponent(g);

            g.setColor(
                    new Color(230,230,230));

            for(int x=0;
                x<getWidth();
                x+=40) {

                g.drawLine(
                        x,
                        0,
                        x,
                        getHeight());
            }

            for(int y=0;
                y<getHeight();
                y+=40) {

                g.drawLine(
                        0,
                        y,
                        getWidth(),
                        y);
            }

            Set<String> drawn =
                    new HashSet<>();

            for(String city1 :
                    graph.keySet()) {

                for(Map.Entry<String,Integer>
                        edge :

                        graph.get(city1)
                                .entrySet()) {

                    String city2 =
                            edge.getKey();

                    String key =
                            city1.compareTo(city2)
                                    < 0

                                    ?

                                    city1 + "-"
                                            + city2

                                    :

                                    city2 + "-"
                                            + city1;

                    if(!drawn.add(key))
                        continue;

                    Point p1 =
                            cityPositions
                                    .get(city1);

                    Point p2 =
                            cityPositions
                                    .get(city2);

               if(shortestPathEdges.contains(key))
    g.setColor(Color.RED);

else if(mstEdges.contains(key))
    g.setColor(Color.GREEN);

else
    g.setColor(Color.BLACK);

                    g.drawLine(
                            p1.x,
                            p1.y,
                            p2.x,
                            p2.y);

                    g.setColor(
                            Color.BLUE);

                    g.drawString(
                            String.valueOf(
                                    edge.getValue()),

                            (p1.x+p2.x)/2,

                            (p1.y+p2.y)/2);
                }
            }

            for(String city :
                    cityPositions.keySet()) {

                Point p =
                        cityPositions
                                .get(city);

                if(city.equals(
                        sourceCity))

                    g.setColor(
                            Color.ORANGE);

                else if(
                        reachableCities
                                .contains(city))

                    g.setColor(
                            Color.GREEN);

                else

                    g.setColor(
                            Color.CYAN);

                g.fillOval(
                        p.x-22,
                        p.y-22,
                        44,
                        44);

                g.setColor(
                        Color.BLACK);

                g.drawOval(
                        p.x-22,
                        p.y-22,
                        44,
                        44);

                g.drawString(
                        city,
                        p.x-18,
                        p.y+5);
            }
        }
    }

    private String getCityAt(
            int x,
            int y) {

        for(String city :
                cityPositions
                        .keySet()) {

            Point p =
                    cityPositions
                            .get(city);

            if(p.distance(
                    x,
                    y) < 25)

                return city;
        }

        return null;
    }

    private void runBFS() {

        if(sourceCity == null)
            return;

        outputArea.append(
                "\n=== BFS ===\n");

        Queue<String> queue =
                new LinkedList<>();

        Set<String> visited =
                new HashSet<>();

        queue.add(sourceCity);

        visited.add(sourceCity);

        while(!queue.isEmpty()) {

            String current =
                    queue.poll();

            outputArea.append(
                    current + "\n");

            for(String next :
                    graph.get(current)
                            .keySet()) {

                if(visited.add(next))
                    queue.add(next);
            }
        }
    }

    private void runDijkstra() {
        shortestPathEdges.clear();

        if(sourceCity == null)
            return;

        Map<String,Integer>
                distance =
                new HashMap<>();
Map<String,String>
        parent =
        new HashMap<>();
        for(String city :
                graph.keySet()) {

            distance.put(
                    city,
                    Integer.MAX_VALUE);
        }

        distance.put(
                sourceCity,
                0);

        PriorityQueue<String>
                pq =
                new PriorityQueue<>(

                        Comparator
                                .comparingInt(
                                        distance::get));

        pq.add(sourceCity);

        while(!pq.isEmpty()) {

            String u =
                    pq.poll();

            for(Map.Entry<String,Integer>
                    edge :

                    graph.get(u)
                            .entrySet()) {

                String v =
                        edge.getKey();

                int weight =
                        edge.getValue();

                int newDistance =
                        distance.get(u)
                                + weight;

                if(newDistance
                        <
                        distance.get(v)) {

                    distance.put(
        v,
        newDistance);

parent.put(
        v,
        u);

pq.add(v);
                }
            }
        }
for(String city :
        parent.keySet()) {

    String p =
            parent.get(city);

    String edgeKey =
            p.compareTo(city) < 0

            ?

            p + "-" + city

            :

            city + "-" + p;

    shortestPathEdges.add(edgeKey);
}
        outputArea.append(
                "\n=== Dijkstra ===\n");

        for(String city :
                distance.keySet()) {

            outputArea.append(
                    city
                            + " = "
                            + distance.get(city)
                            + "\n");
        }
        graphPanel.repaint();
    }
        private void runReachability() {

        if(sourceCity == null)
            return;

        reachableCities.clear();

        Queue<String> queue =
                new LinkedList<>();

        queue.add(sourceCity);

        reachableCities.add(sourceCity);

        while(!queue.isEmpty()) {

            String current =
                    queue.poll();

            for(String next :
                    graph.get(current)
                            .keySet()) {

                if(reachableCities
                        .add(next)) {

                    queue.add(next);
                }
            }
        }

        outputArea.append(
                "\n=== Reachability ===\n");

        for(String city :
                graph.keySet()) {

            outputArea.append(
                    city
                            + " : "
                            + (reachableCities
                            .contains(city)

                            ?

                            "Reachable"

                            :

                            "Not Reachable")
                            + "\n");
        }

        graphPanel.repaint();
    }

    private void runMST() {

        mstEdges.clear();

        if(graph.isEmpty())
            return;

        String start =
                graph.keySet()
                        .iterator()
                        .next();

        Set<String> inMST =
                new HashSet<>();

        Map<String,Integer> key =
                new HashMap<>();

        Map<String,String> parent =
                new HashMap<>();

        for(String city :
                graph.keySet()) {

            key.put(
                    city,
                    Integer.MAX_VALUE);
        }

        key.put(start,0);

        PriorityQueue<String> pq =
                new PriorityQueue<>(

                        Comparator
                                .comparingInt(
                                        key::get));

        pq.add(start);

        int totalCost = 0;

        outputArea.append(
                "\n=== Prim MST ===\n");

        while(!pq.isEmpty()) {

            String u =
                    pq.poll();

            if(!inMST.add(u))
                continue;

            if(parent.containsKey(u)) {

                String p =
                        parent.get(u);

                String edgeKey =
                        p.compareTo(u) < 0

                                ?

                                p + "-" + u

                                :

                                u + "-" + p;

                mstEdges.add(edgeKey);

                int weight =
                        graph.get(p)
                                .get(u);

                totalCost += weight;

                outputArea.append(
                        p
                                + " -- "
                                + u
                                + " : "
                                + weight
                                + "\n");
            }

            for(Map.Entry<String,Integer>
                    edge :

                    graph.get(u)
                            .entrySet()) {

                String v =
                        edge.getKey();

                int weight =
                        edge.getValue();

                if(!inMST.contains(v)
                        &&
                        weight
                                <
                                key.get(v)) {

                    key.put(
                            v,
                            weight);

                    parent.put(
                            v,
                            u);

                    pq.add(v);
                }
            }
        }

        outputArea.append(
                "Total Cost = "
                        + totalCost
                        + "\n");

        graphPanel.repaint();
    }

    public static void main(
            String[] args) {

        SwingUtilities.invokeLater(

                TransportationNetworkAdvanced::new);
    }
}
