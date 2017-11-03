## plz note

This was forked to patch a few smol things to get it running on OTP 20.
May / not work with upstream. 

## Actual README

(Note: Work-in-progress documentation [here](https://github.com/basho/riak_ensemble/blob/develop/doc/Readme.md))

`riak_ensemble` is a consensus library that supports creating multiple
consensus groups (ensembles). Each ensemble is a separate Multi-Paxos
instance with its own leader, set of members, and state.

Each ensemble also supports an extended API that provides consistent
key/value operations. Conceptually, this is identical to treating each
key as a separate Paxos entity. However, this isn't accomplished by
having each key maintain its own Paxos group. Instead, an ensemble
emulates per-key consensus through a combination of per-key and
per-ensemble state.

As mentioned, `riak_ensemble` supports multiple independent consensus
groups. Ensembles are created dynamically, allowing applications to
use `riak_ensemble` in whatever way best fits that
application. Each ensemble also supports dynamic ensemble membership,
using joint consensus to guarantee consistent membership transitions.

A given ensemble is configured to use a particular "ensemble backend".
An ensemble backend is an implemented behavior that defines how a given
peer actually stores/retrieves data. For example, `riak_ensemble`
ships with the `riak_ensemble_basic_backend` which stores data as an
`orddict` that is saved to disk using `term_to_binary`, whereas
`riak_kv` implements the `riak_kv_ensemble_backend` that is used to
interface with Riak's vnodes.

Better documentation is coming soon. For now, this talk from RICON
West 2013 discusses the design of `riak_ensemble` in the context of
adding consistency to Riak 2.0:
http://www.youtube.com/watch?v=gXJxbhca5Xg
