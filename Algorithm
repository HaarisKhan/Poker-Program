from random import *

my_deck = [r + s for r in '23456789JQKA' for s in "CSHD"]

def deal(numhands, n = 5, deck = my_deck):
    shuffle(deck)
    return [deck[n * i: n * (i + 1)] for i in range(numhands)]

def poker(hands):
    "Return the best hand: poker([hand,...]) => hand"
    return allmax(hands, key = hand_rank)

def hand_rank(hand):
    ranks = card_ranks(hand)

    if straight(ranks) and flush(hand):            # Straight Flush
        return (8, max(ranks))
    elif kind(4, ranks):                           # 4 of a Kind
        return (7, kind(4, ranks), kind(1, ranks))
    elif kind(3, ranks) and kind(2, ranks):        # Full House
        return (6, kind(3, ranks), kind(2, ranks))
    elif flush(hand):                              # Flush
        return (5, ranks)
    elif straight(ranks):                          # Straight
        return (4, max(ranks))
    elif kind(3, ranks):                           # 3 of a kind
        return (3, kind(3, ranks), ranks) 
    elif two_pair(ranks):                          # 2 Pair
        return (2, two_pair(ranks), ranks)
    elif kind(2, ranks):                           # Kind
        return (1, kind(2, ranks), ranks)
    else:                                          # High Card
        return (0, ranks)

def card_ranks(hand):
    "Return a list of the ranks, from greatest to least "
   
    ranks = ["--23456789TJQKA".index(r) for r, s in hand]
    ranks.sort(reverse = True)

    if ranks == [14, 5, 4, 3, 2]:
        ranks = [1, 2, 3, 4, 5]
    
    return ranks

def flush(hand):
    """Return True if the suits are all the same"""
    suits = [s for r, s in hand]
    return len(set(suits)) == 1

def straight(ranks):
    """Return True if greatest and least valued card == 4
    and if there are five cards """

    if max(ranks) - min(ranks) == 4 and len(set(ranks)) == 5: 
        return True
    else:
        return False

def kind(n, ranks):
    """Return the first rank that this hand has exactly n of.
    Return None if there is no n-of-a-kind in the hand."""
    for r in ranks:
        if ranks.count(r) == n:
            return r

def two_pair(ranks):
    
    """ Return two ranks as a tuple if there 
    is a two pair (higher, lower). If none,
    return None"""

    pair = kind(2, ranks)
    low_pair = kind(2, list(reversed(ranks)))
    
    if pair and low_pair != pair:
        return (pair, low_pair)
    else:
        return None

def allmax(iterable, key = None):
    """Return the hands of the highest-ranking hand in game IF there is a tie"""
    result = []
    max_val = None

    key = key or (lambda x: x)

    for x in iterable:
        x_val = key(x)
        if not result or x_val > max_val:
            result = [x]
            max_val = x_val
        elif xval == max_val:
            result.append(x_val)

    return result



# Tests

def test():
    "Test cases for the functions in poker program."
    sf = "6C 7C 8C 9C TC".split() # Straight Flush
    fk = "9D 9H 9S 9C 7D".split() # Four of a Kind
    fh = "TD TC TH 7C 7D".split() # Full House
    fl = "3C 9C QC AC 2C".split() # Flush 
    st = "AD 5C 3H 2H 4D".split() # Straight
    tk = "3C 4H 3H 2D 3S".split() # Three of a Kind
    tp = "5S 5D 9H 9C 6S".split() # Two Pairs
    pa = "2S KC 2D AH TS".split() # A Pair
    na = "QD JC KH 2S AD".split() # Nothing

    assert hand_rank(sf) == (8, 10)
    assert hand_rank(fk) == (7, 9, 7)
    assert hand_rank(fh) == (6, 10, 7)
    assert hand_rank(fl) == (5, [14, 12, 9, 3, 2])
    assert hand_rank(st) == (4, 5)
    assert hand_rank(tk) == (3, 3, [4, 3, 3, 3, 2])
    assert hand_rank(tp) == (2, (9, 5), [9, 9, 6, 5, 5])
    assert hand_rank(pa) == (1, 2, [14, 13, 10, 2, 2])
    assert hand_rank(na) == (0, [14, 13, 12, 11, 2])

    return 'tests pass'
