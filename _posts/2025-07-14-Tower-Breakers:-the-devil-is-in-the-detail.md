[The problem](https://www.hackerrank.com/challenges/one-week-preparation-kit-tower-breakers-1/problem?isFullScreen=true&h_l=interview&playlist_slugs%5B%5D=preparation-kits&playlist_slugs%5B%5D=one-week-preparation-kit&playlist_slugs%5B%5D=one-week-day-three)

Read the rules first:

```
Player 1 always move first.
Initially there are n towers.
Each tower is of height m.
The players move in alternating turns.
In each turn, a player can choose a tower of height x
and reduce its height to y, where 1 <= y < x and y evently divides x.
If the current player is unable to make a move, they lose the game. 
```

Given the values of numberOfTowers and towerHeight each, 
determine which player will win. If the first player wins, return 1. Otherwise, return 2.  

which gives

```
1. at the end, the every tower will have the height of 1 (1 <= y < x)
2. y evently divides x, so the divison should have no remainder (modulo result should be 0, tower height can't be a decimal)
3. player 1 move first, and moves in alternating turns, what if the tower height is 1? Player 2 wins.
4. what if the tower is only 1? check if the tower height is 1, player 2 still wins.
5. If the tower height is not 1, say 2, player 1 wins
6. therefore if number of towers are 2, even if the height is not 1, player 2 wins.
7. The winner is the one who leaves the opponent with no available moves. Making the opposition unable to move.
```

hillariously the solutions could be dead simple

```go
func towerBreakers(n int32, m int32) int32 {
    // Write your code here
    if m == 1 || n % 2 == 0 {
        return 2
    }
    return 1
}
```

