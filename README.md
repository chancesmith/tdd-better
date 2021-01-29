# TDD Better
Learning to write tests and the vocabulary of patterns and pitfalls.


## Pitfalls

### Test Fixture
Found out this weekend that the initial data each test starts with is called a [Test Fixture](https://en.wikipedia.org/wiki/Test_fixture). Now we can talk the lingo.
```
test('should make word uppercase', () => {
  // given
  const word = 'special'; // Test Fixture 👈
  const expected = 'SPECIAL';
  // when
  const result = word.toUpperCase();
  // then
  expect(result).toBe(expected)
});
```

### Obscure Test
> An *Obscure Test* is when you’re having trouble understanding the behavior a test is verifying. - [xunitpatterns](http://xunitpatterns.com/Obscure%20Test.html)

A common cause of Obscure Tests is when you have a *Mystery Guest*.
> *Mystery Guest* - The test-reader/developer is not able to see the cause and effect between fixture and verification logic because part of it is done outside the Test Method. - [xunitpatterns](http://xunitpatterns.com/Obscure%20Test.html#Mystery%20Guest)

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
> Sometimes it passes and sometimes it fails - [xunitpatterns](http://xunitpatterns.com/Erratic%20Test.html)

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
