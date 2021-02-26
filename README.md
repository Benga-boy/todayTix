# ASSOCIATE ENGINEER TASK

TodayTix code task

## ANSWER

When creating the lottery ticketing system:

- There will be a number of customers who can enter the draw. For instance, if there were 50 tickets available then 100 people can enter etc

- I may also wish to limit the number of tickets which customers may purchase at any one time to 2 tickets, to make it a fair draw.

- My user model could look something like this:

```JavaScript
User Model
  name: {
    type: String,
    required: true
  },
    email: {
    type: String,
    required: true,
    unique: true
  }
```

- My Ticket model will then look something like this:
Each ticket use has a relationsip with the user
```JavaScript
Ticket Model
    ticket: {
    type: Number,
    required: true,
    unique: true
  },
    user: {
    type: ObjectId,
    ref: 'User'
  }
```

* My algorithm to pick a winner will look something like this:
``` JavaScript
function lotto(tickets, customers) {
  // * Generate random numbers between 1 and the number of tickets available
  const nums = new Set();
  while (nums.size !== tickets.length) {
    nums.add(Math.floor(Math.random() * customers.length) + 1);
  }

  // console.log([...nums].length);

  // The winnin numbers are the randomly generated numbers
  const winningNums = [...nums]

  // console.log(winningNums)

  // To get the winning numbers, I would loop through  my array of tickets and return winning nums that equal to the ticket numbers.
  const winners = tickets.filter(ticket => winningNums.forEach(num => ticket.ticket === num))

  return winners
}
```

## Another outtake - Without constraints on the amount of people that can enter 


* I would keep my user model and ticket models the same. Without limits

* To then pick a winner, I would create a function that picks winners via their index in the tickets array:
``` JavaScript
function lotto(tickets, customers) {
  // * Generate random numbers between 1 and the number of tickets available
  const nums = new Set();
  while (nums.size !== tickets.length) {
    nums.add(Math.floor(Math.random() * customers.length) + 1);
  }

  // console.log([...nums].length);

  // The winnin numbers are the randomly generated numbers
  const winningNums = [...nums]

  // console.log(winningNums)

  // To get the winning numbers, I would return a map of my winning numbers, returning the customer whose index matches given numbers
  const winners = winningNums.map(num => customers[num])

  return winners
}

