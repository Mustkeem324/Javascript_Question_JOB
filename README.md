# Javascript_Question_JOB
## Question1
```
JS newbie "A" wants to learn React from "B" and wants to know in his
network who can introduce him to B in the shortest time period.
INPUT FORMAT
Total Members in Ul Friend Network = N
Memberld1 = N1
Memberld2 = N2
Memberld3 = N3
MemberldN = Nn
Total Possible Edges = E
<Follower 1> <Following 1> <Time taken to send the message> =
p1,q1,t1
<Follower 2> <Following 2> <Time taken to send the message> =
p2,q2,t2
‹Follower 3> <Following 3> <Time taken to send the message> =
p3,q3,3
‹Follower N> <Following N> <Time taken to send the message> =
pn,qn,tn
Follower (Ninja A) = A
Following (JS expert B) = B
OUTPUT FORMAT
Shortest Time A takes to reach B
Sample Input
‹Follower 3> <Following 3> <Time taken to send the message> =
p3,q3,3
‹Follower N> <Following N> <Time taken to send the message> =
pn,qn,tn
Follower (Ninja A) = A
Following (JS expert B) = B
OUTPUT FORMAT
Shortest Time A takes to reach B
Sample Input
4
2
5
7
9
4
2 9 2
7 2 3
7 9 7
9 5 1
7
9

sample output

5 

in js 

```
## Answer1

```
/*
// Sample code to perform I/O:

process.stdin.resume();
process.stdin.setEncoding("utf-8");
var stdin_input = "";

process.stdin.on("data", function (input) {
    stdin_input += input;                               // Reading input from STDIN
});

process.stdin.on("end", function () {
   main(stdin_input);
});

function main(input) {
    process.stdout.write("Hi, " + input + ".\n");       // Writing output to STDOUT
}

// Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
*/
/*Question :
JS newbie "A" wants to learn React from "B" and wants to know in his
network who can introduce him to B in the shortest time period.
INPUT FORMAT
Total Members in Ul Friend Network = N
Memberld1 = N1
Memberld2 = N2
Memberld3 = N3
MemberldN = Nn
Total Possible Edges = E
<Follower 1> <Following 1> <Time taken to send the message> =
p1,q1,t1
<Follower 2> <Following 2> <Time taken to send the message> =
p2,q2,t2
‹Follower 3> <Following 3> <Time taken to send the message> =
p3,q3,3
‹Follower N> <Following N> <Time taken to send the message> =
pn,qn,tn
Follower (Ninja A) = A
Following (JS expert B) = B
OUTPUT FORMAT
Shortest Time A takes to reach B
Sample Input
‹Follower 3> <Following 3> <Time taken to send the message> =
p3,q3,3
‹Follower N> <Following N> <Time taken to send the message> =
pn,qn,tn
Follower (Ninja A) = A
Following (JS expert B) = B
OUTPUT FORMAT
Shortest Time A takes to reach B
Sample Input
4
2
5
7
9
4
2 9 2
7 2 3
7 9 7
9 5 1
7
9

sample output

5 

in js 

*/
class Graph {
    constructor() {
      this.nodes = new Map();
    }
  
    addNode(id) {
      this.nodes.set(id, []);
    }
  
    addEdge(source, target, weight) {
      this.nodes.get(source).push({ target, weight });
      this.nodes.get(target).push({ target: source, weight }); // Assuming undirected graph here
    }
  
    dijkstra(start, end) {
      const visited = new Set();
      const distances = new Map();
      const queue = [];
  
      queue.push({ node: start, distance: 0 });
      distances.set(start, 0);
  
      while (queue.length > 0) {
        queue.sort((a, b) => a.distance - b.distance);
        const { node, distance } = queue.shift();
  
        if (node === end) {
          return distance;
        }
  
        if (visited.has(node)) {
          continue;
        }
  
        visited.add(node);
  
        for (const { target, weight } of this.nodes.get(node)) {
          if (!visited.has(target)) {
            const newDistance = distance + weight;
            if (!distances.has(target) || newDistance < distances.get(target)) {
              distances.set(target, newDistance);
              queue.push({ node: target, distance: newDistance });
            }
          }
        }
      }
  
      return Infinity; // No path found are there 
    }
  }
  
  function shortestTimeToReachB(N, members, E, edges, A, B) {
    const graph = new Graph();
  
    for (let i = 1; i <= N; i++) {
      graph.addNode(members[i - 1]);
    }
  
    for (let i = 0; i < E; i++) {
      const [follower, following, time] = edges[i];
      graph.addEdge(follower, following, time);
    }
  
    return graph.dijkstra(A, B);
  }
  
  // Sample Input putiing 
  const N = 4;
  const members = [2, 5, 7, 9];
  const E = 4;
  const edges = [
    [2, 9, 2],
    [7, 2, 3],
    [7, 9, 7],
    [9, 5, 1],
  ];
  const A = 7;
  const B = 9;
  
  // Output answer
  const result = shortestTimeToReachB(N, members, E, edges, A, B);
  console.log(result); 
  

```

### Question2

```

The Nagging React newbie
A Nagging React newbie "B" is constantly troubling React exp
React Expert "A" needs to know the minimum set of people fol
him he needs to remove from his network to stop "B" from rea
out to him.
INPUT FORMAT
Total Members in Ul Friend Network = N
Memberld1 = N1
Memberld2 = N2
Memberld3 = N3
MemberldN = Nn
Total Possible Edges = E
<Follower 1> < Following 1>
<Follower 2> < Following 2>
<Follower N> < Following N>
Followor = A

Following = B
OUTPUT FORMAT
Set of memberld "A" needs to block
samle input:
4
2
5
7
9
4
2 9
7 2
7 9
9 5
7
9

sample output:
2 7
```

### Answer2


```
function getMembersToBlock(N, members, E, edges, followerA, followingB) {
    const adjacencyList = {};
    for (let i = 0; i < E; i++) {
        const [follower, following] = edges[i];
        if (!adjacencyList[follower]) {
            adjacencyList[follower] = [];
        }
        adjacencyList[follower].push(following);
    }

    const visited = {};
    const queue = [followingB];
    while (queue.length > 0) {
        const current = queue.shift();
        visited[current] = true;
        if (adjacencyList[current]) {
            for (const neighbor of adjacencyList[current]) {
                if (!visited[neighbor]) {
                    queue.push(neighbor);
                }
            }
        }
    }

    const membersToBlock = [];
    for (const member of members) {
        if (!visited[member] && member !== followerA) {
            membersToBlock.push(member);
        }
    }

    return membersToBlock;
}

// Sample input
const N = 4;
const members = [2, 5, 7, 9];
const E = 4;
const edges = [
    [2, 9],
    [7, 2],
    [7, 9],
    [9, 5],
];
const followerA = 7;
const followingB = 9;

// Get the result
const result = getMembersToBlock(N, members, E, edges, followerA, followingB);

// Output the result
console.log(result.join(' '));

```
#### Question3

```
Find Reachability
JS newbie "A" wants to check if he can reach out to a React expert
"B" using his network of React developers. If he can then return 1 else
return O.
INPUT FORMAT
Total members in React Developer Community = N
Memberld1 = N1
Memberld2 = N2
Memberld3 = N3
MemberldN = Nn
Total possible edges = E
< follower 1 (member ID)> <following 1 (member ID)> = u1,v1
‹follower 2 (member ID)> <following 2 (member ID)> = u2,v2
< follower N> <following N> = un, vn
Follower = A
Following = B
OUTPUT FORMAT
If A can reach B then output is 1, else 0.

sample input 

4
2
5
7
9
4
2 9
7 2
7 9
9 5
7
9


sample output 

1
```

#### Answer3

```
function canReach(N, members, E, edges, follower, following) {
    const graph = {};

    for (let i = 0; i < E; i++) {
        const [followerId, followingId] = edges[i];
        if (!graph[followerId]) {
            graph[followerId] = [];
        }
        graph[followerId].push(followingId);
    }

    function dfs(node, target, visited) {
        if (node === target) {
            return true;
        }

        visited.add(node);

        if (graph[node]) {
            for (const neighbor of graph[node]) {
                if (!visited.has(neighbor) && dfs(neighbor, target, visited)) {
                    return true;
                }
            }
        }

        return false;
    }

    const visited = new Set();
    return dfs(follower, following, visited) ? 1 : 0;
}

const N = 4;
const members = [2, 5, 7, 9];
const E = 4;
const edges = [
    [2, 9],
    [7, 2],
    [7, 9],
    [9, 5],
];
const follower = 7;
const following = 9;

const result = canReach(N, members, E, edges, follower, following);
console.log(result); //result should be 1



```
