# Códigos utilizados para implementar localdbs no NEO4J

O intuito é demonstrar em grafos como funciona o blockchain e suas recompensas


## Criando os nodes

### Criar o bloco 1
```
create(b:block{
    blockhash: '00000000000003e690288380c9b27443b86e5a5ff0f8ed2473efbfdacb3014f3',
    version: 536870912,
    prevblock: '000000000000050bc5c1283dceaff83c44d3853c44e004198c59ce153947cbf4',
    merkleroot: '64027d8945666017abaf9c1b7dc61c46df63926584bed7efd6ed11a6889b0bac',
    timestamp: 1500514748,
    bits: '1a0707c7',
    nonce: 2919911776,
    size: 748959,
    txcount: 1926
})
```

### Criar o bloco 2
```
create(b:block{
    blockhash: '474337f9064b66cf22ad806ca47e177d80306790dad086530e668f23ef7e53d2',
    version: 536870912,
    prevblock: '00000000000003e690288380c9b27443b86e5a5ff0f8ed2473efbfdacb3014f3',
    merkleroot: '7f2867d9cf2619347b10be5ea75d3c9a1796a63aa97729bac87469f883b98d32',
    timestamp: 1500514748,
    bits: '1a0707c7',
    nonce: 3119911776,
    size: 748959,
    txcount: 1926
})
```

### Criar o coinbase, referenciando o blockhash do bloco e sua recompensa
```
create(btc:coinbase{
	blockhash:'00000000000003e690288380c9b27443b86e5a5ff0f8ed2473efbfdacb3014f3',
	reward:6.500
})
```

### Relacionar Coinbase (recompensa bitcoin)
```
MATCH
 (b:block),
 (btc:coinbase)
WHERE b.blockhash = btc.blockhash
    CREATE (b)-[r:REWARD]->(btc)
```

### Relacionar um bloco com o outro bloco anterior
Relacionar Outro bloco
```
MATCH
 (b:block),
 (b2:block)
WHERE b.blockhash = b2.prevblock
    CREATE (b)-[r:PREVBLOCK]->(b2)
```
