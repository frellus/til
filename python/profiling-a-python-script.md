# Profiling A Python Script

If you want to profile a Pythong script then cPython is easy to use to find where a program is spending the most time.

## JSON example

I have a script to process a list of JSON events, one per line in a file. A 300MB file is taking around 7 seconds to process the events. Where is the program spending its time?
```
greg:fleetlog greg$ time ./fleetlog testdata/test-big.json -q 
Displayed 310686 of 310686 events read.

real	0m7.822s
user	0m6.972s
sys	    0m0.830s
```

Let's call cProfile on it:
```
python3 -m cProfile ./fleetlog testdata/test-big.json -q > profile.txt
```

The `profile.txt` has all the information we need on where we're spending our time. For example:
```
         3511061 function calls (3510888 primitive calls) in 6.868 seconds

   Ordered by: standard name

   ncalls  tottime  percall  cumtime  percall filename:lineno(function)
    16/15    0.000    0.000    0.004    0.000 <frozen importlib._bootstrap>:1009(_handle_fromlist)
       11    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:103(release)
        9    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:143(__init__)
        9    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:147(__enter__)
        9    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:151(__exit__)
       11    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:157(_get_module_lock)
        9    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:176(cb)
        2    0.000    0.000    0.000    0.000 <frozen importlib._bootstrap>:194(_lock_unlock_module)
     19/6    0.000    0.000    0.036    0.006 <frozen importlib._bootstrap>:211(_call_with_frames_removed)
```
(etc.)

Looking down in the detailed output we see one line which stands out in terms of time:
```
   310686    4.928    0.000    4.928    0.000 decoder.py:343(raw_decode)
```

This is related to the json module. Now I know that processing the file isn't slow because of disk , for example. It's related to marshaling JSON!
