# Exported names in golang

As Go newbie, I wrote a function yet it wasn't accessible from main package. It turned out that in Go, a name is exported if it begins with a capital letter. For example, `Pizza` is an exported name, as is `Pi`, which is exported from the `math` package. `pizza` and `pi` do not start with a capital letter, so they are not exported.



