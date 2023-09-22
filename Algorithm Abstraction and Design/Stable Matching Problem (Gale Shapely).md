Given sets A & B, and functions $f_{a} : A x B \rightarrow \mathbb{R}$ & $f_{b} : B x A \rightarrow \mathbb{R}$,

Find a bijective function from $A \rightarrow B$ where there are not pairs $(a,b)(a',b')$ where 

- $a, a' \in A, b, b' \in B, a \neq a', b \neq b'$

1. **Sets \(A\) and \(B\)**: Imagine two boxes. One box contains elements from set \(A\) and the other from set \(B\). 

2. **Functions \($f_a$\) and \($f_b$\)**: You have two machines (functions). 
   - \($f_a$\) takes one item from each box (from \(A\) and \(B\)), and it outputs a number (from the set of real numbers).
   - \($f_b$\) also takes one item from each box, but in the reverse order, and it too gives you a number.

3. **Bijective function**: Now, you want to connect each item in box \(A\) with exactly one item in box \(B\), such that no item is left out or doubly connected. This connection is like pairing up dance partners; every person from group \(A\) dances with exactly one person from group \(B\), and vice versa.

4. **Condition**: This is the tricky part. Imagine you've picked two different pairs of dancers: 
   - \(a\) from group \(A\) with \(b\) from group \(B\)
   - \(a'\) from group \(A\) with \(b'\) from group \(B\)
   
   Your condition says that if you put these pairs into the \($f_a$\) or \($f_b$\) machines, no pair should give the same number as output. That means every unique pair has its own unique dance step (number) that no other pair can reproduce.

## Hospital Problem 

Given a preference list of $n$ hospitals & $n$ students, find a matching without an "unstable" pair
###### Gale Shapely Algorithm Structure

Initialize M as an empty array
	Hospital H is unmatched
	s $\leftarrow$ first student
		if unmatched
			add as matching
		elif s prefers hospital to current match
			replace match
		else
			replace H

## Proof of Termination

Hospitals propose in decreasing order

Once proposed, students only "trade up"

#### Claim: Algorithm terminates after $n^2$ iterations of the while loop

###### Proof : Each time through a while loop, a hospital proposes to at most n new students. Thus, there are max $n^2$ possible proposals

**Proof of Termination:**

1. **Max Proposals Per Hospital:** A hospital will propose to each student at most once. This is because once a hospital has proposed to a student, it will never propose to that student again (whether accepted or rejected). Hence, each hospital can propose to at most n students (given there are $n$ students).

2. **Total Proposals:** Since there are n hospitals, and each can propose to at most n students, the maximum number of proposals that can be made is \( $n^2$ \).

3. **Trade Up Mechanism:** Once a student gets a proposal, they either remain unmatched or they "trade up". Meaning, they will never "trade down" to a less preferred match in any future iterations. This means that each time a hospital gets rejected, it's permanent and the hospital will move on to the next student on its list.

4. **Exhaustion:** A hospital will only remain unmatched if it has exhausted its preference list without finding a match. Since each hospital can only run through its preference list once, and there are \( $n$ \) hospitals, we're assured that all hospitals will be done proposing after \( $n^2$ \) proposals.

5. **Conclusion:** Considering the above points, each hospital can propose at most \( $n$ \) times and there are \( $n$ \) hospitals, hence there can be at most \( $n^2$ \) proposals. After \( $n^2$ \) proposals, every hospital will have either found a match or exhausted its list of students to propose to. Therefore, the algorithm will terminate after at most \( $n^2$ \) iterations of the while loop.

#### Proof of Correctness - Perfect Match

###### Claim : Gale Shapely outputs $\underline{a}$ matching

###### Proof: 
- Hospitals propose only if unmatched $\Rightarrow$ matched to $\leq$ 1 student
- Student keeps only best hospital $\Rightarrow$ matched to $\leq$ 1 hospital

###### Claim: In Gale-Shapely matching, all hospitals get matched

###### Proof [by contradiction]
- Suppose that some hospital $h$ is unmatched upon termination
- Then some student $s$ is unmatched on termination
	- By this above observation, said student was never proposed to
	- but $h$ proposed to $s$, since $h$ is unmatched, thus $\Rightarrow\Leftarrow$

###### Proof of Correctness - stability
###### Claim: There are no unstable pairs consider any pair $h$-$s$ that is not in M*

###### Case: h never proposed to $s$ 
- $h$ prefers current partner $s'$ to $s$
- $h$ $-$ $s$ is not unstable

###### Case: $h$ proposed to $s$
- $s$ rejected $h$ ($s$ has a better option)
- $s$ prefers Gale-Shapley partner $h'$ to $h$
- $h - s$ is not unstable

in both cases the pair $h-s$ is not unstable

# Observations of Said Algorithm

##### The Gale Shapely Algorithm which has hospitals iterate through students list is hospital-optimal

###### Proof:
- Assume that the matching is not optimal
- This means that there exists a Hospital $h$ that is not matched with its best <u>valid</u> partner $s$ in $M'$  (highest student with a stable match)
- This also means that $h$ is rejected by $s$ during the gale-shapely matching
- When $s$ rejects $h$, $s$ forms a commitment to the hospital $h'$, who $s$ prefers to $h$
- Let $s'$ be the partner of $h'$ in $M$
- $h'$ has not been rejected by any valid partner at the point where $h$ is rejected to $s$, thus $h'$ has not yet proposed to $s'$ when $h'$ proposed to $s$ 
	- $h'$ prefers $s$ to $s'$
	- but this means that $h'$ prefers $s$ to $s'$ and $s$ prefers $h'$ to $h$
	- Thus, $h' - s$ is unstable in $M$, a contradiction
##### The Gale Shapely Algorithm is also student-pessimal
###### Proof:
- Suppose $h-s$ matched in $M'$ but $h$ is not the worst valid partner for $s$
- There exists a stable matching $M$ in which $s$ is paired with a hospital, say $h'$, whom $s$ prefers less than $h$
	- This means that $s$ prefers $h$ to $h'$
- Let $s'$ be the partner of $h$ in $M$
- This means that $s$ is the best valid partner for $h$ by the previously proved hospital-optimality
- This means that $h$ prefers $s$ to $s'$
- Thus, $h$ prefers $s$ to $s'$ and $s$ prefers $h$ to $h'$, meaning $h$ and $s$ could elope and $h-s$ is an unstable pair

#### Extensions
###### Matching M is unstable if there is a hospital h and students s such that 
- $h$ and $s$ are acceptable to each other
- Either $s$ is unmatched or $s$ prefers $h$ to assigned hospital; and
- Either $h$ does not have all its places filled, or $h$ prefers $s$ to at least one of its assigned students

Theorem. There exists a stable matching
Straightforward generalization of the Gale Shapely Algorithm