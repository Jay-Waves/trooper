Trooper, currently under development, is a self-use value mutation tool designed
to enhance our fuzzer's effectiveness. It operates by receiving seeds
(interpreted as byte streams -> uint8 arrays) from an input seed pool and
applies subtle modifications to them. I have incorporated a variety of [mutation
methods](mutation_method.md) into Trooper. The decision-making process for
selecting these mutation methods is outsourced to an external fuzz server. In
more detail, the fuzzer supplies Trooper with seeds along with a set of
['knobs'](knobs.md), which are essentially weightings assigned to the different
mutation methods. Trooper then employs these weightings to probabilistically
determine the mutation technique to apply, subsequently returning the altered
seeds.

It's important to note that Trooper is agnostic to the mechanism of iterating
over the knobs; it merely accepts them from the calling process. The fuzzer
using Trooper should continuously monitor the behavior of the program under
fuzzing test, adjusting the knobs based on this observed behavior.

seed (byte array) and knobs -> trooper -> mutated seeds (mutants) 