#! /usr/bin/env python

import sys

def stacks(n):
    return sh(n, 2)

def sh(n, mn):
    if n < 2:
        return []
    elif n == 2:
        return [[n]]
    else:
        return [ [h] + tails
                    for (h, t) in [ (i, n-i) for i in range(mn, 1+n/2) ]
                        for tails in sh(t, h)
        ] + [[n]]

def print_solutions(sl):
    for i, s in enumerate(sl):
	print 'solution %s: %s' % (i+1, s)

def main(argv):
    n = int(argv[1])
    print 'N:', n
    solutions = stacks(n)
    print '%s solutions' % len(solutions)
    print_solutions(solutions)

if __name__ == '__main__':
    main(sys.argv)
