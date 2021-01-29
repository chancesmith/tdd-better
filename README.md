# tdd-better
Learning to write tests and the vocabulary of patterns and pitfalls.


## Pitfalls

### Obscure Test
> An *Obscure Test* is when you’re having trouble understanding the behavior a test is verifying.

A common cause of Obscure Tests is when you have a *Mystery Guest*.
> *Mystery Guest* - The test-reader/developer is not able to see the cause and effect between fixture and verification logic because part of it is done outside the Test Method.

```
const NAME = 'Spencer Moore';

test('should first name', () => {
  // given
  const expected = 'Spencer';
  // when
  const result = getFirstName(NAME); // NAME is the Mystery Guest 👈
  // then
  expect(result).toBe(expected)
});
```

### Erratic Test
> Sometimes it passes and sometimes it fails

This was an example from FunFact.

```
const NAME = 'Spencer Moore';
test('should first name', () => {
  // given
  const team = ['Adam', 'Alex', 'Brantley'];
  const expected = ['Alex', 'Adam', 'Brantley'];
  // when
  const result = shuffleArray(team); // Erratic Test 👈
  // then
  expect(result).toBe(expected)
});
```

*Fix:* unless there is 0 or 1 item in the array, prevent `shuffleArray()` from ever giving back the array back in the same order.
