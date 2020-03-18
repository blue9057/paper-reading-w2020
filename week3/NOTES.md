# Week 3 Reading Notes

## Basic CFI (2005)
- CF Hijacking vulnerable instructions include `call *%rax`, `jmp *%rax`, `ret`
- Requires control flow diagram to be made for the given program
- Originally, uses a set of valid targets, and checks control flow changes against this set
- Authors also experimented with function cookies
- CF can be 'bent' as any target in the valid set target is an acceptable destination
- Requires source code

## BinCFI (2013)
- Coarse Grained CFI - less 'good' than the original (2005)
- Return can return anywhere after a call
- Authors claimed 99% reduction of attacks, though all is needed to make a successful attack is one gadget
  - Unless your claim about defense includes ROP, it is not really security
- Overall, an imprecise defense

## IFCC (2014)
- Controls the forward and backward edges of the CF graph
- Is focused on where CF is going

## CCFI (2015)
- Uses HMAC with better crypto instructions to encrypt pointers 
- On return, decrypts and checks pointers
- Does not enforce CFI, really


## PiCFI (2015)
- PiCFI becomes as bad as the original (2005), as it takes in (read: considers) user input. 
  - Specifying user input can allow you to expand the set of targets to the whole range
- Dynamically increases the set of valid destination targets, but does not reduce it

## uCFI (2018)
- Analyzes what the unique target can be - only one valid target
- Detects paths taken on previous executions to make a single path
  - Similar to, but not the same as Intel PT
  
## CPI (2014)
- Wants to protect the forward and backwards edges of CF graph
  - Backwards edge already protected by Shadow Stacks
- Breaks code memory into three sections
  - [CPS] or [CP] (at a secret address; holds code ptrs)
  - [SS]
  - [Data] (calls f(x) through CPS section
- All pointers must o to the CPS recursively
- There exist cases where many inherited objects (OOP Concepts) can break this; Similar attack to that against COOP

## COOP (2015)
- Use weird tricks with OOP to induce failures in defenses

## CFB (2015)
- 'Bend' control flow based on the set of available, valid targets. 
- No direct hijacking, but you can choose from the set of acceptable targets

## Newton (2017)
- Assume arbitrary write to known location

## IH (2016)
- Most Shadow Stacks and Code Pointer Stashes (CPS) require 'hiding' things
- Can be broken by mapping contiguous chunks of memory and finding where allocation does not occurr
  - In those spaces, there be dragons.
  
