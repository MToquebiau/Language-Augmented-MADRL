# Language-Augmented-MADRL

## Compared approaches

The training script can be launched with different algorithms for learning communication, controlled by the `comm_type` argument that can be set as:

**Main approaches:**
* `no_comm`: No communication at all. This equates to learning with MAPPO. 
* `language_sup`: Agents learn to use a given pre-defined language by training the language modules on language tasks (captioning and CLIP).
* `perfect`: Agents communicate with the "perfect" (because using the language as we intended) messages given the oracle.
* `emergent_continuous`: Agents learn with emergent communication using continuous signals as messages. Because all computation is differentiable, they learn differentiable emergent communication to maximise their own return **and** the returns of other agents. The dimension of the communicated vectors is defined by the `context_dim` argument.
* `emergent_discrete_lang`: Agents learn with emergent communication using discrete symbols. "lang" indicates that these agents can generate sequences of messages, just like when using the pre-defined language (i.e., same size of vocabulary and maximum length of generated sentences). During training, agents use the **Gumbel softmax** to generate tokens, allowing to learn differentiable emergent communication.

**Ablations:**
* `obs`: Agents communicate their local observation to other agents.
* `no_comm+lang`: Agents do not communicate but they learn the language modules anyway, allowing to have some grounding of representation learning in language concepts.
* `perfect+no_lang`: Agents communicate "perfect" messages given by the oracle, but they do not have gradients from language tasks flowing into the agents' policy. They do not learn the decoder. They do learn a language encoder in order to encode the incoming messages, but no gradients from RL flow into the language encoder. 
