---
title: "Concorrência: Exemplo prático"
author: fziliotti
date: 2024-02-29 04:33:00 +0800
categories: ["Desenvolvimento"]
tags: [frontend, backend]
---

## Introdução

Esse post pois um exemplo bacana de como estudar com o ChatGPT, primeiro eu queria estudar concorrência, depois pensei numa situação fictícia e depois solicitei ao chatgpt para me ajudar a criar esse post. Com o código gerado e após fazer algumas modificações, achei legal compartilhar o resultado aqui no meu blog.

###  Concorrência
A concorrência é uma peça chave na programação moderna, permitindo que diversas tarefas sejam executadas simultaneamente, otimizando o desempenho e melhorando a eficiência do software. Para ilustrar essa abordagem, vamos explorar o fascinante mundo da concorrência através de um cenário delicioso: uma pizzaria em Go!

### Exemplo: Pizzaria
Imagine uma pizzaria movimentada, onde diferentes pedidos estão chegando constantemente. Cada pedido representa uma tarefa a ser executada: preparar uma pizza com um sabor específico. 

Vamos desbravar como a concorrência em Go pode ser aplicada nesse contexto, garantindo que as pizzas sejam preparadas de forma eficiente e deliciosa.

### Exemplo de implementação

```go
package main

import (
  "sync"
	"fmt"
	"time"
)

type Pedido struct {
	Sabor string
	Tempo int
}

// Função para simular o tempo de preparo de cada pizza
func prepararPizza(sabor string, tempoPreparo int, pizzaria chan<- string) {
	fmt.Printf("Preparando pizza de %s...\n", sabor)
	time.Sleep(time.Duration(tempoPreparo) * time.Second)
	pizzaria <- sabor
}

func main() {
	pizzaria := make(chan string) // Canal para pedidos de pizza
	var wg sync.WaitGroup         // Wait Group para esperar todas as goroutines

	// Lista de pedidos da pizzaria
	pedidos := []Pedido{
		{"margherita", 3},
		{"pepperoni", 5},
		{"quatro queijos", 4},
		{"calabresa", 6},
		{"vegetariana", 4},
	}

	// Inicia goroutines para preparar cada pizza
	for _, pedido := range pedidos {
		wg.Add(1) // Adiciona 1 pedido ao contador do WaitGroup
		go func(p Pedido) {
			prepararPizza(p.Sabor, p.Tempo, pizzaria) // Inicia o preparo de uma pizza
		}(pedido)
	}

	// Goroutine para esperar todas as pizzas ficarem prontas e fechar o canal
	go func() {
		wg.Wait()           // Espera que todas as goroutines chamem Done()
		close(pizzaria)     // Fecha o canal após todas as pizzas ficarem prontas
		fmt.Println("Pizzas prontas :)")
	}()

	// Loop para imprimir as pizzas preparadas
	for sabor := range pizzaria {
		fmt.Printf("Pizza de %s está pronta.\n", sabor)
		wg.Done() // Remove um contador do wait group
	}
}

```

### Goroutines: Os Pizzaiolos Paralelos

Em Go, goroutines são como os pizzaiolos ágeis, capazes de trabalhar simultaneamente sem interromper o fluxo principal do serviço. Cada pedido é uma goroutine que pode ser processada de maneira independente, proporcionando uma experiência paralela.

### Canais: A Comunicação entre a Cozinha e o Atendimento

Os canais em Go são como o sistema de pedidos e entregas da pizzaria. Eles fornecem uma forma segura de comunicação entre as goroutines. Cada pedido é enviado através de um canal para a cozinha, onde os pizzaiolos trabalham diligentemente.

### Wait Group: A Contagem dos Pedidos
O Wait Group é como a contagem de pedidos pendentes. Ele garante que a pizzaria não feche antes de todas as pizzas serem preparadas. Cada goroutine adiciona um pedido à contagem, e ao finalizar, ela sinaliza que o pedido foi atendido.