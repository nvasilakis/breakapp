# BreakApp

Developers today make pervasive use of third-party modules to reduce costs and accelerate release cycles, at risk to safety and security.
`breakapp` exploits module boundaries to automate security-oriented compartmentalization of legacy applications and enforce security policies, enhancing reliability and security.
It transparently spawns modules in protected compartments while preserving their original behavior.
Optional high-level policies decouple security assumptions made during development from requirements imposed for module composition and use.
These policies allow fine-tuning trade-offs such as security and performance based on changing threat models or load patterns.
Experimental results demonstrate feasibility by enabling simplified security hardening of existing systems with low performance overhead.

Read more about the problem and approach in our [PLOS17](http://nikos.vasilak.is/pubs/breakapp:plos:2017/) or [NDSS18](http://nikos.vasilak.is/pubs/breakapp:ndss:2018/) papers;
  if you have developed useful BreakApp policies, feel free to submit a [pull request](https://github.com/andromeda/breakapp).
