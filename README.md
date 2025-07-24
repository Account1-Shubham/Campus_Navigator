🧭 Campus Indoor Navigation System
📌 Overview
This project provides an indoor navigation system that allows users to find the shortest path between rooms and locations inside a campus building. It is particularly useful for new visitors, students, or staff who find it difficult to locate rooms due to the complex layout of large buildings (like colleges, hospitals, or malls).

The system handles both horizontal navigation (on the same floor) and vertical navigation (via stairs). It uses Dijkstra’s algorithm to find the shortest path between two nodes (locations) and gives step-by-step directions, including information about stairs and directional turns.

📁 Features
📍 Add named locations with floor coordinates (x, y, z)

🛣️ Add walking paths (edges) between rooms with distances

🪜 Add stairs between floors

📐 Compute shortest path using Dijkstra’s algorithm

📄 Show clear, human-friendly instructions: "Turn Left", "Go Straight", "Go upstairs", etc.

🧱 Code Structure
🔹 Data Structures
cpp
Copy
Edit
struct Edge {
    string to;
    int dist;
    string type; // "walk" or "stairs"
};

struct Position {
    int x, y, z; // z represents floor number
};
Edge: Represents a connection (walkable or stairs) between two nodes.

Position: Holds 3D coordinates of a node (room).

🧭 Class: CampusNavigator
A class that manages the campus map and navigation.

Public Methods
addNode(name, x, y, z) – Adds a location with its coordinates.

addWalkEdge(a, b, dist) – Adds a bidirectional walking path between two nodes.

addStairEdge(a, b) – Adds a bidirectional stair path (floor changing).

showPath(src, dst) – Uses Dijkstra’s algorithm to find and display the shortest route.

Private Method
computeTurn(prev, cur, next) – Computes direction of turn using vector cross product. Returns "Go Straight", "Turn Left", or "Turn Right".

🧮 Pathfinding Logic (Dijkstra)
cpp
Copy
Edit
priority_queue<pair<int, string>, vector<>, greater<>> pq;
Maintains minimum distance from src to all nodes.

Traverses nodes and updates paths using edge costs.

Special handling for stairs (0 distance but floor change).

Reconstructs path using parent pointers.

📢 Direction Output Format
Start from: "Start at X -> proceed to Y (Z steps)"

Midway: "Proceed from X to Y (Z steps) -> Turn Left/Right/Go Straight"

On stairs: "At X: Go upstairs to Floor Z"

Final: "You have arrived at <destination>"

🧪 Sample Locations (Node Map)
The current setup models the ground floor (z = 0) of a campus:

📍 Main Gate → Reception → Corridor

➡️ Right wing (G1–G14 classrooms, AV room, basketball court)

⬅️ Left wing (G15–G28, Library, Washroom)

🪜 Stairs at both left and right wings

🧑‍💻 Sample Usage
cpp
Copy
Edit
int n;
cin >> n;
while(n--) {
    cout << "Enter start node exactly: ";
    getline(cin, start);
    cout << "Enter destination node exactly: ";
    getline(cin, dest);
    nav.showPath(start, dest);
}
User is prompted to input the start and end nodes.

System returns path directions with total step count.

🚧 Known Limitations
❌ No GUI – purely command-line

❌ Only one floor is implemented

❌ Assumes static building layout

✅ Future Enhancements
🌐 Add multi-floor support with lift/elevator

🗺️ Add a GUI using SFML or Qt

📱 Create Android app version using Kotlin/Java

📡 Add real-time location tracking via Bluetooth beacons or QR codes

🧾 Example Output
vbnet
Copy
Edit
Directions from Reception to G10:
- Start at Reception -> proceed to Corridor Recp (12steps)
- Proceed from Corridor Recp to G14 (8steps)  -> Turn Right
- Proceed from G14 to G1 (4steps)  -> Turn Right
- Proceed from G1 to G13 (3steps)  -> Go Straight
...
- At TR01 Stairs: Go downstairs to Floor 0
**You have arrived at G10**
Total distance: 97 STEPS
