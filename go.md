- Don't try wait for a metric you expect to be 0. Make another metric which will be non 0 in this scenario, or do something else.
- If you are using mutexes and you have early returns in your function, you need to be careful that you unlock on the early return as well.
- If your code is getting stuck and you are using waitgroups, ensure the number of calls to `wg.Add()` is equivalent to the number of calls to `wg.Done()`.
- Make sure channels have enough capacity for what you expect them to hold / are you sure you want to send to an unbuffered channel?
- Are you looping over a map and expecting the same result every time? Don't
- Do you want to create a table test where the struct field you want to assert changes per test case? Then in the test table, one of the fields should a function which takes in the struct, and returns a specific field in the struct.
   ```go
   tt := map[string]struct{
     field func(*someStruct) int
   }{
     "case 1": {
       field: func(s *someStruct) int { return s.thisField },
     },
     "case 2": {
       field: func(s *someStruct) int { return s.thatField },
     },
   }
   ```
