# Portal

Use Portal Gun to send data from one door to another

## How to use

Example in the console local:

```text
iex> Portal.shoot(:orange)
{:ok, #PID<0.72.0>}
iex> Portal.shoot(:blue)
{:ok, #PID<0.74.0>}
iex> portal = Portal.transfer(:orange, :blue, [1, 2, 3, 4])
#Portal<
       :orange <=> :blue
  [1, 2, 3, 4] <=> []
>

iex> Portal.push_right(portal)
#Portal<
    :orange <=> :blue
  [1, 2, 3] <=> [4]
>
```

Distributed

`iex --sname room1 --cookie secret -S mix`

```text
iex(room1@COMPUTER-NAME)> Portal.shoot(:blue)
{:ok, #PID<0.65.0>}
```

`iex --sname room2 --cookie secret -S mix`
```text
iex(room2@COMPUTER-NAME)> Portal.shoot(:orange)
{:ok, #PID<0.71.0>}
iex(room2@COMPUTER-NAME)> orange = {:orange, :"room2@COMPUTER-NAME"}
{:orange, :"room2@COMPUTER-NAME"}
iex(room2@COMPUTER-NAME)> blue = {:blue, :"room1@COMPUTER-NAME"}
{:blue, :"room1@COMPUTER-NAME"}
iex(room2@COMPUTER-NAME)> portal = Portal.transfer(orange, blue, [1, 2, 3, 4])
#Portal<
  {:orange, :room2@COMPUTER-NAME} <=> {:blue, :room1@COMPUTER-NAME}
          [1, 2, 3, 4] <=> []
>
iex(room2@COMPUTER-NAME)> Portal.push_right(portal)
#Portal<
  {:orange, :room2@COMPUTER-NAME} <=> {:blue, :room1@COMPUTER-NAME}
             [1, 2, 3] <=> [4]
>
```