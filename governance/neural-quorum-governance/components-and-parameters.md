# Components & Parameters

NQG is modeled after neural networks and leverages layered voting neurons that dynamically adjust voting weights based on a participant’s expertise, trust earned from peers, and historical contributions to SCF (Neural Governance). Additionally, NQG has a flexible delegation model inspired by the Stellar Consensus Protocol (Quorum Delegation), enabling users to delegate votes to a group rather than a single individual.

* [Neural Governance](components-and-parameters.md#id-1.-neural-governance)
* [Quorum Delegation](components-and-parameters.md#id-2.-quorum-delegation)

## 1. Neural Governance

Neural Governance is a modular framework used in the Stellar Community Fund for assigning voting power to community members based on their reputation, expertise, and historical contributions. It is inspired by the structure of neural networks, where simple components (neurons) are connected and layered to create complex and adaptable systems.

### **1.1. How Neural Governance Works**

Neural Governance uses the abstractions of Voting Neurons, which are arranged and aggregated together in layers. Each Voting Neuron represents an independent piece of logic on how a User's Voting Power should be defined and consists of:

* An Oracle Function, which encodes the core logic.
* A Weighting Function, which encodes how it should be weighted.

The outputs from all Voting Neurons are aggregated together in layers, and then passed as an input to the next layer, until a final value is reached.

<figure><img src="/.gitbook/assets/nqg/neural-governance-framework.png"/></figure>

Neural Governance at a glance: In this stylized implementation, User Vote Power starts with a default voting power (such as zero), which gets replaced by the voting power that is computed by aggregating the Reputation and Past Voting Neurons' weighted outputs. This is then fed to the Trust Neuron, which will then provide the Final User Vote Power.

The rationale for this design is the fact that Voting Neurons allow for encoding a comprehensive set of power determinants, which enables a divide-and-conquer approach towards setting up incentives without requiring an overly complex monolithic function:

* **Plug-and-Play Neurons**: New neurons can be added to the system to capture additional dimensions of user behavior or community goals.
* **Weight Adjustment**: The influence of each neuron can be adjusted over time through governance processes, allowing the system to evolve based on community needs.
* **Transparency**: Each neuron's contribution to a user's voting power is transparent and explainable, ensuring trust in the system.

### **1.2. Voting Neurons used in SCF**

Neural Governance uses Voting Neurons to compute a user's voting power. Each neuron represents a specific aspect of a user's contribution or reputation within the community. These neurons are layered and aggregated to produce a final voting power score.

The key neurons in the initial implementation are:

* [Assigned Reputation](components-and-parameters.md#id-1.1.2.1.-verified-tier-and-discord-roles-neuron)
* [Voting History](components-and-parameters.md#id-1.1.2.2.-voting-history-neuron)
* [Voting Quality](components-and-parameters.md#id-1.1.2.3.-vote-quality-neuron)
* [Trust Graph](components-and-parameters.md#id-1.1.2.4.-trust-graph-neuron)
* [Trust Loss](components-and-parameters.md#id-1.2.4.-trust-loss-neuron)

<figure><img src="/.gitbook/assets/nqg/new-neurons-setup.png"/></figure>

Out of the above, the Trust Graph Neuron carries significant relative weight. With Quorum Delegation, this makes SCF’s governance mechanism primarily trust-based. This has been a deliberate choice from the beginning, as SCF’s existing community prior to implementing NQG had been based on trust informally, and because ‘human trust’ has the capability to bridge multiple forms of reputation (e.g. quality of contributions, engagement within a community, and general sense), and can thus manage complexity of the system. Managing complexity is important in NQG, because the more neurons (data inputs) you add, the more parameters and weighting attribution methods you need to adjust, the more chance of unclarity and confusion on how the system calculates the final vote.

Weight attribution methods of each Neuron in SCF’s implementation are designed to mimic natural reputation attribution and learning curves so there’s a clear path for new users to gain voting power, prevent indefinite voting power attribution and power centralization), as well as allowing the community to collectively decrease voting weight of bad actors.

#### **1.2.1. Assigned Reputation (Verified Tier & Discord Roles) Neuron**

**Purpose**: Rewards users for demonstrating expertise and active participation in the Stellar Community Fund, specifically Discord.

**Mechanism**: Users earn verified tiers (Pathfinder, Navigator, Pilot) based on their contributions to the Stellar Community Fund, associated with their Discord account. Learn more about how verified tiers are earned here. Users get additional points for having specific discord roles.\
\
**Weight is added in a linear fashion**:

| Discord Role            | Weight Bonus |
| ----------------------- | ------------ |
| SCF Verified            | 0.0          |
| SCF Pathfinder          | 1.0          |
| SCF Navigator           | 2.0          |
| SCF Pilot               | 3.0          |
| Ambassador President    | 1.0          |
| SCF Project             | 1.0          |
| Public Good Contributor | 1.0          |
| Moderator               | 1.0          |
| SDF                     | 1.0          |
| Tier 1 Validator        | 1.0          |
| \[Region] Ambassador    | 0.5          |

{% hint style="info" %}
**Example**: A user with the "Pilot" rank receives a higher bonus than a user with the "Pathfinder" rank.

A user with “Navigator” rank and “SCF Project” role receives 2.0 + 1.0 = 3.0 bonus.
{% endhint %}

#### **1.2.2. Voting History Neuron**

**Purpose**: Encourages consistent voting participation.

**Mechanism**: Uses a logistic function to calculate a bonus based on a user's voting history. Recent active participation is weighted more heavily, and the bonus saturates over time to prevent long-term members from having an indefinite advantage

**To calculate the Voting History Neuron Bonus**:

{% stepper %}
{% step %}
**Round Weight Assignment as input to bonus calculation**

Each round a voter participated in gets assigned a weight through a logistic curve.

$$
y = a+( k - a )(c + q * e(-b*(x - o)) )(1/n)
$$

<sup><sub>This formula was proposed by BlockScience (learn more about requirements and parameters<sub></sup> [<sup><sub>here<sub></sup>](https://hackmd.io/@blockscience/SkBilx67A) <sup><sub>and the parameter effects of<sub></sup> [<sup><sub>logistical curves on Wikipedia<sub></sup>](https://en.wikipedia.org/wiki/Generalised_logistic_function)<sup><sub>).<sub></sup> <sup><sub>_a_<sub></sup> <sup><sub> </sup><sup><sub>= the left horizontal asymptote,<sub></sup> <sup><sub> </sup><sup><sub>_k_<sub></sup> <sup><sub> </sup><sup><sub>= the right horizontal asymptote,<sub></sup> <sup><sub> </sup><sup><sub>_c_<sub></sup> <sup><sub> </sup><sup><sub>= 1,<sub></sup> <sup><sub> </sup><sup><sub>_q_<sub></sup> <sup><sub> </sup><sup><sub>= is related to the value<sub></sup> <sup><sub> </sup><sup><sub>_Y_<sub></sup><sup><sub>(0),<sub></sup> <sup><sub> </sup><sup><sub>_b_<sub></sup> <sup><sub> </sup><sup><sub>= the growth rate,<sub></sup> <sup><sub> </sup><sup><sub>_n_<sub></sup> <sup><sub> </sup><sup><sub>= affects near which asymptote maximum growth occurs,<sub></sup> <sup><sub> </sup><sup><sub>_o_<sub></sup> <sup><sub> </sup><sup><sub>= X axis offset (current round # - 10),<sub></sup> <sup><sub> </sup><sup><sub>_x_<sub></sup> <sup><sub> </sup><sup><sub>= current round #<sub></sup>

In the graph below, we chose arbitrary values (a = 0, k = 1, c = 1, q = 1, b = 1, n = 4, o = `[current_round - 8]`) to add mild effects influenced by round importance over the number of rounds. Weights for each round a user voted in are multiplied by that user's percentage of active votes. It is set to always be at least 50%, because not all tiers are allowed to vote actively. 

Additionally, if you are a team member of a project that's being voted on in a given round, you are not allowed to vote, but this neuron treats you as if you had voted 100% actively, so you don't lose your participation bonus.

<figure><img src="/.gitbook/assets/nqg/round-weight-graph.png"/></figure>

{% hint style="info" %}
Example: User A voted in round 42, from the graph above we can see weight for this round is 1.0. In this round user A submitted 68 Yes/No votes, and 32 Delegate votes, so 68% active votes. The final weight of round 42 for this user will be 1.0 x 68% = 0.68.

User B voted in round 42, from the graph above we can see weight for this round is 1.0. In this round user B submitted 0 Yes/No votes, and 100 Delegate votes, so 0% active votes. The final weight of round 42 for this user will be 1.0 x 50% = 0.5.
{% endhint %}
{% endstep %}

{% step %}
**The sum of the weights of all rounds participated in is passed as the input to a logistic curve.**

$$
y = a+( k - a )(c + q * e(-b*(x - o)) )(1/n)
$$

<sub>_a_</sub> <sub></sub><sub>= the left horizontal asymptote,</sub> <sub></sub><sub>_k_</sub> <sub></sub><sub>= the right horizontal asymptote,</sub> <sub></sub><sub>_c_</sub> <sub></sub><sub>= 1,</sub> <sub></sub><sub>_q_</sub> <sub></sub><sub>= is related to the value</sub> <sub></sub><sub>_Y_</sub><sub>(0),</sub> <sub></sub><sub>_b_</sub> <sub></sub><sub>= the growth rate,</sub> <sub></sub><sub>_n_</sub> <sub></sub><sub>= affects near which asymptote maximum growth occurs,</sub> <sub></sub><sub>_o_</sub> <sub></sub><sub>= X axis offset,</sub> <sub></sub><sub>_x_</sub> <sub></sub><sub>= Sum of Rounds Weights.</sub>

In the graph below, we chose arbitrary values (a = (k/e^5), k = 3, c = 1, q = 1, b = 1, n = 1, o = 5) to add mild effects to the Voting History bonus influenced by the number of rounds.

<figure><img src="/.gitbook/assets/nqg/voting-history-output-bonus.png"/></figure>

{% hint style="info" %}
Example: Alice has voted in 5 rounds: SCF#32, 34, 36, 42, 44. We look at the first graph, take the corresponding weight for each round, and apply the active voting bonus for each round. Assume Alice always votes 100% actively, so we get values 0.375, 0.6, 0.85, 1.0, 1.0. We sum the weights and get a value of 3.825. Then we look at the second graph for the value of 3.825 at the X axis, and see that on the Y axis the corresponding bonus will be 0.75 — this is Alice’s Voting History Neuron bonus. 

Now let's look at Bob who has also voted in 5 rounds, but more recently in SCF#40, 41, 42, 43, 44. For each of those rounds weight is almost 1.0, approximately summing up to 5.0. Looking at the second graph, Bob’s Voting History Neuron’s bonus will be 1.4. Even though both Alice and Bob voted in 5 rounds, recent rounds get more of the Voting History bonus.
{% endhint %}
{% endstep %}
{% endstepper %}

#### **1.2.3. Vote Quality Neuron**

**Purpose**: Validates the quality of previous votes.

**Mechanism**: Creates a retroactive performance bonus based on the completion rate of previously voted on and awarded projects.

For every project that a voter has actively voted for and has been selected to be awarded since SCF #30,

For any given user since SCF #30, we go over all votes of given user, since round #30, and check what is the current status of awarded projects he voted for. Depending on it, points are added or subtracted. If a project is:

* Live on Stellar within 6 months: 0.3
* Live on Stellar after 6 months: 0.1
* Not live on Stellar within 6 months, Awarded -0.3
* Not live on Stellar within 6 months, MVP -0.2
* Not live on Stellar within 6 months, Testnet -0.1

This applies to active Yes votes. Delegated votes that resolve to Yes through the user's quorum earn half the points of an active Yes vote, rewarding active conviction over passive delegation. Delegated votes that resolve to No or Abstain don't affect the score.

The sum of all points is then passed as the input to a logistic curve, and its output is the final Vote Quality bonus. This means the bonus is always in the range from -5 to 5, so users with a long voting history can't accumulate an unlimited bonus, while the relative ordering between voters is preserved.

$$
y = a+( k - a )(c + q * e(-b*(x - o)) )(1/n)
$$

<sub>_a_</sub> <sub></sub><sub>= the left horizontal asymptote,</sub> <sub></sub><sub>_k_</sub> <sub></sub><sub>= the right horizontal asymptote,</sub> <sub></sub><sub>_c_</sub> <sub></sub><sub>= 1,</sub> <sub></sub><sub>_q_</sub> <sub></sub><sub>= is related to the value</sub> <sub></sub><sub>_Y_</sub><sub>(0),</sub> <sub></sub><sub>_b_</sub> <sub></sub><sub>= the growth rate,</sub> <sub></sub><sub>_n_</sub> <sub></sub><sub>= affects near which asymptote maximum growth occurs,</sub> <sub></sub><sub>_o_</sub> <sub></sub><sub>= X axis offset,</sub> <sub></sub><sub>_x_</sub> <sub></sub><sub>= sum of points.</sub>

In the graph below, we chose values (a = -5, k = 5, c = 1, q = 1, b = 0.4, n = 1, o = 0). The curve is centered on the origin, so a user with no points gets a bonus of exactly 0, and equal sums of positive and negative points result in bonuses that are exact negatives of each other.

<figure><img src="/.gitbook/assets/nqg/vote-quality-curve.png"/></figure>

{% hint style="info" %}
**Example**: In previous rounds, a user voted for one project that went live on Stellar within 6 months, and one that is on Testnet after 6 months, so the sum of his points will be 0.3 - 0.1 = 0.2. We then look at the graph for the value of 0.2 on the X axis, and see that the corresponding bonus is ≈ 0.2 — around zero the curve is almost linear, and it only flattens out for users with a large sum of points.
{% endhint %}

#### **1.2.4. Trust Graph Neuron**

**(Github |** [**Module Brief**](https://hackmd.io/@blockscience/SkBK6x8cJx)**)**

**Purpose**: Encourage users to actively participate in the community, to become more trusted.

**Mechanism**: Each user defines a list of users they trust. Based on those lists we perform some calculations explained below:

* PageRank — calculates an initial trust score based on how many users trust a given user, which is then normalized to a range from 0 to 3 based on the scores of all users.
* Highly Trusted Bonus - additional bonus if given user is trusted by a highly trusted user

<figure><img src="/.gitbook/assets/nqg/trust-graph-neuron.png"/></figure>

**1.2.4.1 Normalized PageRank**

Min-max normalized PageRank algorithm is used to analyze the trust graph formed by community members. Initially each user gets assigned a trust value of 1n (n being number of users)

Then we iterate over all users a 1000 times using the formula below, to get an accurate page rank value.

$$
PR(A) = \frac{1-d}{n} + d \sum_{B \in M(A)} \frac{PR(B)}{L(B)}
$$

<sup><sub>PR(A) - page rank value for user A, d - damping factor, in our case 0.85 (typical, commonly used value), n - number of users, BM(A) - some other user B that belongs to the set of all users trusting user A, PR(B) - page rank value for user B, L(B) - number of users trusted by user B<sub></sup>

So for user A, we take 1-dn, add our damping factor multiplied by the sum of all trust scores of users trusting our user A, divided by how many users they trust. This means that trust from someone trusting less users is worth more.

After that we perform a min-max normalization to ensure that scores of all users are distributed between 0.0 and 3.0.

#### **1.2.4.2 Highly Trusted Bonus**

After calculating PageRank scores, we take users with top 10% scores, those are considered highly trusted individuals. Then for each highly trusted user, we take the list of users they trust, and give everyone an additional bonus of 15% of their own score. If someone is trusted by multiple highly trusted users, he will get this bonus multiple times.

Note: Keep in mind that even though we perform normalization after the PageRank, adding this HTB can result in the trust score of some users being higher than 3.0. This is an important change from the original implementation of the system, which was designed in a way so all 3 neurons should output values in range 0.0 - 1.0. We believe this isn't a flaw, because it makes the trust have a bigger impact on the overall NQG score, which is desired.

#### **1.2.5. Trust Loss Neuron**

The Trust Loss Neuron tracks how a person's reputation changes between voting rounds by watching how many users stop trusting them, and can generate only 0 or negative outputs. If many community members removed you from their trust list since the last round, your score goes down by one point for each person who did. If nobody withdrew their trust, your score doesn’t change. Output from this neuron is also added to your NQG score, and is not tied to the Trust graph.

### **1.3. Calculating Final Neural Governance Score**

After all 5 neurons are calculated, the results are aggregated together to give a final voting power. We aggregate results of neurons in a single Layer:

| Layer # | Neurons                                                         | Aggregator Type | Explanation                       |
| ------- | --------------------------------------------------------------- | --------------- | --------------------------------- |
| Layer 1 | <p>Trust Graph</p><p>Assigned Reputation</p><p>Vote Quality</p><p>Prior Voting History</p><p>Trust Loss</p> | Sum             | Adds results of all neurons       |


The result of Layer 1 is equal to the final voting power. In the future, we might extend the system to use another layer with a different aggregator.

***

## 2. Quorum Delegation

Quorum Delegation is a novel delegation mechanism that allows users to delegate their voting power to a group of trusted individuals (a quorum) rather than a single delegate. This approach reduces user attention costs and the risk of centralization and collusion while allowing high flexibility in delegation.

### **2.1. How Quorum Delegation Works**

Quorum Delegation (QD) allows users to passively vote by delegating their choice to a group of users. Unlike traditional delegation (1:1), QD allows distributed delegation across multiple users.

1. Delegating members choose and rank a set of delegates.
2. If enough ranked delegates actively vote, their decision forms a Quorum Vote automatically for the user. If not enough ranked delegates actively vote,
3. The outcome of the Quorum Vote is weighted by the delegating member’s voting weight, and sent as input for the final vote tally.

<figure><img src="/.gitbook/assets/nqg/delegations-logic.png"/></figure>

In the example above, the quorum consists of 10 anonymous users of which 6 vote "Yes", 2 vote "No", 1 abstains, and 1 does not participate. The quorum participation threshold is 3/5 (6 users). Since "Yes" exceeds a simple majority (4 votes), the user automatically votes "Yes".

SCF’s implementation of NQG does not allow redelegation of delegating members who don’t actively vote themselves to keep accountability of active voting members and ensure a sufficient number of active voters on each funding decision. Should the number of voting members grow, we may eventually allow redelegation up to a certain amount of hops.

#### **2.1 Definitions of Quorum Delegation in SCF**

* **Delegating Member**: User with Pathfinder, Navigator, or Pilot tier that has selected to delegate a particular vote instead of actively voting for or against a proposal (Pathfinders can only delegate, not vote actively).
* **Quorums**: Delegating members create a delegate list or quorum (only [SCF Build Open Track](../../scf-awards/build-award/open-track.md) projects go through community vote).
* **Delegate**: User with Pilot tier that has nominated themselves to be a delegate as part of the [Quarterly Governance Process](../../scf-awards/build-award/quarterly-governance-process.md).

#### **2.2. Current Parameters of Quorum Delegation in SCF**

The current implementation of QD in SCF has fixed parameters with relatively light thresholds to optimize for vote throughput. Some context: in rounds with SCF v5.0 and earlier, we saw a high amount of Abstain votes due to delegating members not actively voting. Lower parameter thresholds in combination with the Category-Specific Delegate nomination process have significantly improved delegate vote throughput.

<table><thead><tr><th>Parameter</th><th width="355.34375">Description</th><th>#</th></tr></thead><tbody><tr><td>Min Quorum Candidates</td><td>Minimum size of potential candidates a user must select for their Quorum</td><td>7</td></tr><tr><td>Max Quorum Candidates</td><td>Maximum size of potential candidates a user can select for their Quorum</td><td>15</td></tr><tr><td>Quorum Participation Threshold</td><td>Minimum % of quorum participants needed for a valid vote</td><td>7</td></tr><tr><td>Quorum Size</td><td>Max number of candidates considered in a Quorum Vote</td><td>15</td></tr><tr><td>Agreement Threshold</td><td>Minimum % of agreement for Yes required among active votes</td><td>66.67%*</td></tr></tbody></table>

<sub>\*has changed in past few rounds depending on Abstain rate.</sub>

**Example Scenario**

{% hint style="info" %}
**Example Scenario:**

1. Alice (who is a Navigator) chooses to delegate her vote to a quorum of 7 delegates.
2. During a voting round, 5 delegates of the quorum vote "Yes," and 2 delegates vote "No."
3. Since the quorum meets the consensus threshold (66%), Alice's vote (with her own voting power assigned through Neural Governance) is counted as "Yes."
{% endhint %}

#### **2.2.1. Understanding the difference between the purpose of Trust Graph Neuron and Quorum Delegation**

The relationships within the Trust Graph Neuron show correlations with Quorum Delegation as both are focused on trust, but each have a distinct purpose — while it might be assumed that a user would add their delegates to their trusted list of users, they would not necessarily select everyone in their trusted list as delegates (and not everyone would be available, as delegate selection happens quarterly based on nomination).

Trust in the Trust Graph Neuron is expected to be assigned more liberally — a user can assign trust for any reason to help gain reputation for that user, as there is no direct effect on their own choices and voting power. Similarly, a user can assign trust to a high number of other users, while Quorum Delegation is limited.
