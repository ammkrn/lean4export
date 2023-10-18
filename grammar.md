
# Export format grammar

NOTE: users should initialize names[0] as the anonymous name, and levels[0] as universe zero.

For clarity, some of the compound items are decorated here with a name, for example `(name : T)`, but they appear in the export file as just an element of `T`.

Example export files can be found in `examples` at the top level of this repository.

```
File ::= Item*

Item ::= Name | Universe | Expr | RecRule | Declaration

Declaration ::= Axiom | Quotient | Definition | Theorem | Inductive | Constructor | Recursor

nidx, uidx, eidx, ridx ::= nat

Name ::=
  | nidx "#NS" nidx string
  | nidx "#NI" nidx nat

Universe ::=
  | uidx "#US"  uidx
  | uidx "#UM"  uidx uidx
  | uidx "#UIM" uidx uidx
  | uidx "#UP"  nidx

Expr ::=
  | eidx "#EV"  nat
  | eidx "#ES"  uidx
  | eidx "#EC"  nidx uidx*
  | eidx "#EA"  eidx eidx
  | eidx "#EL"  Info nidx eidx
  | eidx "#EP"  Info nidx eidx eidx
  | eidx "#EZ"  Info nidx eidx eidx eidx
  | eidx "#EJ"  nidx nat eidx
  | eidx "#ELN" nat
  | eidx "#ELS" (hexhex)*

Info ::= "#BD" | "#BI" | "#BS" | "#BC"

Hint ::= "O" | "A" | "R" nat

RecRule ::= ridx "#RR" (ctorName : nidx) (nFields : nat) (val : eidx)

Axiom ::= "#AX" (name : nidx) (type : eidx) (uparams : uidx*)

Def ::= "#DEF" (name : nidx) (type : eidx) (value : eidx) (hint : Hint) (uparams : uidx*)
  
Theorem ::= "#THM" (name : nidx) (type : eidx) (value : eidx) (uparams: uidx*)

Quotient ::= "#QUOT" (name : nidx) (type : eidx) (uparams : uidx*)

Inductive ::= 
  "#IND"
  (name : nidx) 
  (type : eidx) 
  (numParams: nat) 
  (numConstructors : nat) 
  (ctorNames : nidx {numConstructors}) 
  (uparams: uidx*)

Constructor ::= 
  "#CTOR"
  (name : nidx) 
  (type : eidx) 
  (parentInductive : nidx) 
  (numParams : nat)
  (constructorIndex : nat)
  (numFields : nat)
  (uparams: uidx*)

Recursor ::= 
  "#REC"
  (name : nidx)
  (type : eidx)
  (k : 1 | 0)
  (numParams : nat)
  (numIndices : nat)
  (numMotives : nat)
  (numMinors : nat)
  (numRules : nat)
  (recRules : ridx {numRules})
  (uparams : uidx*)
```
