# Notes on AI realization (pre-paradigm)
`Dec 2014`

This is Keng's personal note on the essential ideas to realize AI, from the perspective of Computer Science, Quantum Physics, Mathematics and Philosophy.

The note is pre-paradigm, i.e. written just before the author has rigorously studied the subject and adopted the paradigm of the field. This is so that the author have a chance to ponder before conforming to the conventional way of thinking about the subject. 

We write this note as a mathematician, foundational quantum physicist, and beginning computer scientist. Thus, the "realizable" ideas of AI here imply physics-mathematical realizability. This pre-paradigm work shall be compared to its post-paradigm counterpart, and the discrepancies be scrutinized, to see why some physically plausible ideas are in practice impossible, or vice versa.


## Origin of this Work
`Dec 2014`

The idea first started in Summer 2014 at the Perimeter Institute for Theoretical Physics, when the author discussed the definition of intelligence with his colleagues. The discussion was influenced by their background in quantum physics and quantum information/computation. 

Later, when the author was delving in computer science and doing theoretical math, the idea came into mind: "Can a computer do proofs like a mathematician?" 






## Scratch

Pain and the foundation of fear 

Evolutionary instincts

Paradigm breaking: how should AI do it?

Stimuli dampening for AI


Many aspects of the human mind evolves from natural selection, and sexual activities, ie to attract mates and procreate. 

Let AI play games
Jenga
Recoverable memory 
Bootstrap

Humanly things:
Believe and hope - religion


mutation theory: humans are not literal because we are flexible – we can mutate information.

what is language? a set of protocols for exchanging information?

new section: post-C human features, as inspiration to what the super-ToC shd have.

The limitation/bound of Boolean-classical paradigm: AI impossible here as implied by Godel's Theorem

Consciousness and autonomy 

As long as we stay in the Boolean - classical paradigm, creating an AI is impossible, by Gödel's Thm. 

Jack asked a vital question: why do we need feelings, and as we developed, why do they get richer and not the opposite?
Are these what give us purposes? The sense of achievement, motivation, curiosity etc. So is it necessary to stimulate these hormonal-chemical perceptions in AI too?

The development of a conscious, intelligent entity – must it require us treating it like evolutionary being?

Timescale: baby to mature mind
Prehistoric to modern human
Progressive enhancement, develop AI like develop human mind. Slowly encode and build up more complex thinking/feeling


Or notice how humans build the math. What ideas are necessary precursor to others. Also we tend to work from the complex, i.e. Simpler theorems are much harder, and takes longer time to proof.
If one can build a super computer that's intelligent enough to start from scratch and re proof and rebuild all maths humans have done, and outpace us. 


Reconciliation/error correction. Get several contradictory things and try to  optimize for most logically sound, least contradictory. Like how humans can recover from mistakes by inferencing from several external facts. 
Doubt 
More features of human thinking. 

Paradigm 
So to teach a being or a computer to think, whenever there's a thought there's a paradigm. Humans are bad at changing their paradigms, but if we can make computers change that quickly as needed, omg who knows what new theories they can invent. 





| Chapters |
|:---------|
| *[Working Definition](#Working Definition)* |
| *[Feasibility Assumptions](#Feasibility Assumptions)* |
| *[Gödel's Incompleteness Theorem and the Limit of Computers](#Godel)* |
| *[The Theoretical Constraints](#The Theoretical Constraints)* |



## <a name="Working Definition"></a>Working Definition
`Dec 2014`

We do not yet have a rigorous working definition of AI. However, as a preliminary, we assumed a flexible, vague idea of Artificial Intelligence; and do not yet attempt to define it rigorously, until the main idea has taken a sufficiently mature form.

Currently, by AI we generally mean a sufficiently complete simulation of the human mind, i.e. an entity that can think, is conscious, and can deceive human beings (the Turing test). These are however dangerous words, and we shall not attempt to delve deeper.

#### Loose Definition
Artificial Intelligence is for now loosely defined as man-made entity which can mimic the functionality of a human brain, i.e. manifests `intelligence` and passes the Turing test, effectively deceiving humans. Shortly, to create an AI is to simulate a human mind. Note that we use computers and AI interchangeably, as once an AI is realized on a computer, we can update the definition of computers correspondingly.

Whereas `intelligence` is defined as the ability to obtain, process and utilize information, then carry out strategies to achieve certain aims.



## <a name="Feasibility Assumptions"></a>Feasibility Assumptions
`Dec 2014`

From the standpoint of physics, the human brain is an assemblage of highly ordered matter which can be reconstructed if given a complete blueprint. The human brain shall be seen as a superset of the definition of computers that is more universal than the Universal Turing Machine. In principle, if one can sufficiently replicate the neuro-structure of the human brain, together with necessary input/output (perception/action) interface, then one can simulate a fully-functional human mind, i.e. intelligence.

It is intuitive that since the human brain, as all matters in the universe, obeys the same physics, the application of these laws guarantees the feasibility of reproducing an intelligent, conscious entity. It is then up to us to reverse-engineer the human brain and its perceptual/responsive extensions to obtain a blueprint for AI.



#### The Difference between a Computer and a Human Mind
The gap between the capability of a computer and a functional human mind is too wide – computers are built of a simplistic model of logic and math, and are restricted by deterministic, macroscopic(classical) physical laws; whereas the human mind is capable of randomness and creativity, and is believe to operate on the level of quantum physics.

As of this time, computers are defined through automata and the Universal Turing machine. On the surface, computers do calculations algorithmically; while human minds seem to operate with randomness and free will.

Consider the next generalization of computers by this: when is a human's thinking most like a computer, i.e. most strictly logical. Doing mathematical proofs immediately came to mind – it is a combination of human creativity and strict logic. This seems an easier leap than to have a computer start doing art like a human.

Therefore, think of how humans do math proofs, and try to classify the types of proofs/theories can and cannot be done by computers. Gödel's theorem immediately comes up.


## <a name="Godel"></a>Gödel's Incompleteness Theorem and the Limit of Computers
`Dec 2014`

This was one of the first crucial ideas we encountered in a series of "disappointing" discoveries on artificial intelligence. Closely related to the present model of computers, Gödel's Theorem of mathematical logic states that a theory cannot be both consistent and complete. In its common application to replicating the human mind, computers are consistent and therefore incomplete; whereas humans are inconsistent and thus incomplete. This underscores a fundamental difference between the nature of computers and humans. Thus, the next generalization/update of the definition of a computer shall resolve this incompatiblity: i.e. make computers inconsistent and complete. This gives us the first two criteria for a generalization of a computer:

```
1. Update to accommodate quantum randomness.
2. Update to be complete and inconsistent in the Godel sense.
```





## <a name="The Theoretical Constraints"></a>The Theoretical Constraints
`Dec 2014`

We discuss the theoretic constraints of modern computers from the view point of Computation theory, our research of super-theories at Perimeter Institute, and some inference from Godel's Incompleteness Theorem.

The modern theory of computation (abbreviated ToC) is founded on the paradigms of Finite Automata/Universal Turing Machine and Shannon's Information theory, both of which are classical – as in classical, non-quantum physical.


#### Hierarchy of Theories
Now we study ToC as a theory, outline its relations with more general theories, see where it stands, and where can we go next. When we study theories, we study their scopes and limits. For any theory, call it *A*, its sub-theory *inf-A* (for *infimum-A*) is a smaller subset often more limited in scope, is a branch, is an application, is a cruder approximation. For example, Newtonian mechanics is a sub-theory of Einstein's Relativity.

Likewise, the super-theory *sup-A* (or *supremum-A*) is a more general theory which contains *A*, and perhaps more. It is more general, refined and precise. For example, quantum theory is super-classical; by decoherence it reduces to the cruder, macroscopic classical approximation. It also has non-classical aspects – entanglement.

Going back to ToC, it is a sub-theory of classical physics and mathematics. In short, we build computers by applying physics and exploiting properties of matter, to effectively simulate a UTM that behaves consistently with boolean logic.

One can more carefully reorder the hierarchy and see ToC as a sub-theory of classical physics, and classical physics a sub-theory of mathematics. We view mathematics as the ancestral-super-theory, i.e. all physical theories ultimately is a subset of it. We argue this is justified despite the seeming fact that physics is drawn upon not only math, but also the a-priory laws of nature. However, all physical theories are applications of mathematics, and this is increasingly clear as efforts at Perimeter Institute and elsewhere are underway to rewrite the foundations of physics with complete math-rigor.


#### New Physics, New ToC

Computers are built by the application of physics, or more specifically, classical physics. The physics employed gives the power, and imposes physical limitations. That is to say a physics gives rise to a ToC – imagine in a parallel universe where the physical laws are different; the inhabitants would build their own different computers that adhere to their physics.

The idea that new physics can give rise to new ToC may be foreign to many; it is only because the computers haven't existed long enough to experience paradigm changes in physics. Therefore, we are still stuck with version 1.0 of the computer.

However, the first revolution is coming – computers lived through the advent of quantum physics. It didn't take long before people realized one could do computation using quantum physics. What followed was quantum computation-information theory – the new ToC, or computer 2.0. We shall call it quantum-ToC. There is still much to be done, and people are still trying to fully understand it.

Some claim that quantum computers will not be starkly different from the classical ones, and its potential may only be in some very specific applications such as factoring problems. Well, this isn't really that surprising. Quantum physics isn't too different from classical physics either, at least from the standpoint of quantum foundations.

Quantum foundations, as the name tells, is the study of the foundations of quantum physics. Our group at Perimeter Institute tackles it from a rather interesting perspective: quantum computations. Instead of doing ToC using physics, we use ToC to do physics. The main subject is correlations, which is used to study the scopes and limits of classical, quantum and even post-quantum physics using bits constructed in these paradigms. The foundational framework was correlation theory and general causal theory, built primarily by Tobias Fritz and Matthew Pusey.

In our work, we realized the difficulty in distinguishing between classical and quantum physics. In fact, there is only very few known correlations that are purely-quantum, non-classical.

#### Hierarchy of ToCs
The study of correlation using general bits also hints at the possibility of a super-quantum theory – theory more general than quantum physics. This may then supply a new physics for computer 3.0, or super-ToC.

Overall, we now have the hierarchy of possible ToCs, corresponding to different physical theories:

`classical-ToC < quantum-ToC < super-ToC`

Overall, the hierarchy of theories now look like (letting `C` = classical physics, `Q` = quantum):

` ToC < C < Q-ToC < Q < super-ToC < super-Q < math `

Furthermore, we can assume there exists a complete physical theory that can fully and consistently describe the whole universe. This is the "completeness" of a physical theory. Whatever this final complete theory is, it is a strict super set of quantum theory, as we know that quantum theory is still incomplete, and inconsistent with general relativity.


#### The Completeness Criterion
Godel's Incompleteness Theorem provides a crucial test to the scope of any theory, i.e. a theory is either complete or consistent, but never both. Most critically, it allows us to tell if a theory is general enough to account for the functioning of the human mind.

The criteria lies in completeness – humans make mistakes, thus are inconsistent, hence are complete. Modern computers are the opposite; they follow strict machine logic, thus are consistent and incomplete. This hints that we are still a long way from a ToC that can effectively simulate a human mind – call it the human-ToC. Perhaps it should better be called a ToT, Theory of Thinking. However the task at hand is to generalize the modern definition of computation, thus the name stays.

Godel's theorem therefore provides a criterion for the human-ToC we want – it must be complete (thus inconsistent). Going back to the hierarchy of ToCs above, it implies this super theory must be general enough to include the human mind as a sub-theory. We are not sure if human-ToC will lie between super-Q and Math, or beyond Math.

`super-Q < human-ToC < math` or `super-Q < math < human-ToC`

We make a remark regarding placing human-ToC as beyond super-quantum. Human brain is part of the physical world, and must therefore obey the true physical laws described by some complete physical theory. So, we can derive a ToC (theory of mind) off this complete theory, and this shall enable us to realize AI. Given that, the next natural step is to discover this super theory.

In our study of correlations, there exists a lot of super-quantum correlations, and thus potentially many general super-quantum theories. Our method is by constructing classes of setups within the limitations of a theory to prove or disprove the inclusion of a correlation by the theory. For example, the Bell's correlation can be proven to be outside of classical theory, and realizable within quantum theory, because the quantum setups employ entanglement – its non-classical feature. 

Here's an idea we haven't rigorously tried – for the super-quantum correlations, instead of using quantum bits in the setups, we can try `using humans`. If humans can account for some super-quantum correlations, this would be a major leap. However as of know we do not clearly know what even does "using humans" for the setup mean. This is an interesting topic for future exploration.


#### How close to completion is our ToC?
Is our ToC complete enough to realize AI? Since by AI we mean a sufficient simulation of the human mind, we can ask if our ToC can describe the human mind.

Is human thinking classical? We are definitely hardwired by our experience in the macro world to form some strong classical intuition. We think very classically; this is why quantum physics is so hard for us. 

What are some features of human thinking that are not classical? Our capability of randomness and free will immediately comes to mind. Certainly, we are unlike clockwork that runs deterministically on classical laws – that is free will; in fact, we can break off any classical trajectory as we wish – that is pure randomness. Is it also very fair to suspect that the innerworking of the human mind is purely quantum.

The answer to this may come from the Human Connectome Project. Once we have successfully probed and simulate a complete human mind, the level of ToC required to do that will give us the answer. However, by Godel's theorem, it is likely that our classical ToC would not be sufficient.


This concludes our discussion on theoretical constraints.




## Post-Classical Human Features
We enumerate the possible human features that are post-classical, i.e. those that cannot be accounted for by classical physics and its ToC. These shall be some inspirations for what the super-ToC should encompass.

#### Ability to do math proofs (some types)
especially, dealing with infinities.
Out of the context of computable, decidable, halting problems.

#### More generally, ability to think, whatever it means



#### Randomness (pure randomness, manifest of quantum physics)

#### Gödel's Completeness and Inconsistency
non-literal as machines


dangerous terrain:
#### Consciousness and Free Will (Autonomy)

#### Feelings
synonymous with consciousness?
Consciousness => emotions
Converse may be false?
test for consciousness: put subject in front of the mirror; test for self identification.


#### Creativity and Idea Synthesis; idea-Mutation:
need a mutation theory??

#### Ability to adapt and evolve (reconciliation and error correction)




from the standpoint of information theory ?

`What else are indispensable?:`
#### I/O: perception
#### feelings




## Questioning the completeness
Questioning the completeness of the mathematical paradigm:
i.e. is Math complete for achieving our purpose – all of our treatments employ math and thus are confined within the paradigm.
Is math the ultimate complete system needed to describe the occurences in the universe, including the human mind?
Physics shows this to be likely the case: If math completely describes all of the universe, it shall too describe its constituents either as sub theories.

Conjecture thus relies on the completeness of physical theory, and Math is bigger than physics.

Or if not, proof by contradiction:
Name a thing that cannot be mathematically formalized, and prove so. question too ambiguous.



