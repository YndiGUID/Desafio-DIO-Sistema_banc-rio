# Desafio-DIO-Sistema_bancario

import datetime

movimentacoes = []
saques_diarios = 0
saldo = 0
data_ultimo_saque = datetime.date.today()
limites_saques_diarios = 3
limite_valor_saques = 500
    
def mostar_extrato(Movimentacoes):
    if movimentacoes:
        print("Extrato da conta:")
        for transacao in movimentacoes:
            print(transacao)
        
    else:
        print("Nenhuma movimentação realizada.")

def mostrar_saldo(Saldo):
    print(f"Seu saldo atual é: R${saldo:.2f}")
    
def menu_inicial():
     saldo = 0
     saques_diarios = 0
     data_ultimo_saque = datetime.date.today() 

     print("Bem-vindo ao Banco Python!")
     
while True:

    opcao = input("\nSelecione a operação desejada:\n1 - Extrato\n2 - Depósito\n3 - Saque\n4 - Sair\n")
    
    if opcao == "1":
        mostar_extrato(movimentacoes)
        mostrar_saldo(saldo)     
    elif opcao == "2":
        valor_deposito= input("Informe o valor do depósito: R$")
        try:
            valor_deposito = float(valor_deposito)  
            if (valor_deposito > 0):
                saldo += valor_deposito
                now = datetime.datetime.now()
                movimentacoes.append(f"Depósito de R$ {valor_deposito:.2f} realizado em {now.strftime('%d/%m/%Y %H:%M:%S')}")
                print(f"Operação realizada com sucesso! Seu saldo atual é de R$ {saldo:.2f}")
            else:
                print("Operação falhou! O valor informado é inválido.")
        except ValueError:
            print("Por Favor, insira um número válido.")
    elif opcao == "3":
        today = datetime.date.today()
        if today != data_ultimo_saque:
            saques_diarios = 0 
            data_ultimo_saque = today

        if saques_diarios >= limites_saques_diarios:
            print("Operação falhou! Limite de saques diários excedido.")
            continue
    
        valor_saque = input("Informe o valor do saque: R$ ")
        try:
            valor_saque = float(valor_saque)
            if valor_saque > limite_valor_saques:
                print(f"O limite por saque é de R$ {limite_valor_saques:.2f}"  'tente novamente.')
            elif valor_saque > saldo: 
                print (f"Operação falhou! Saldo insuficiente. seu saldo atual é de R$ {saldo:.2f}")
            else:
                saldo -= valor_saque
                saques_diarios += 1
                now = datetime.datetime.now()
                movimentacoes.append(f"Saque de R$ {valor_saque:.2f} realizado em {today.strftime('%d/%m/%Y %H:%M:%S')}")
                print(f"Operação realizada com sucesso! Seu saldo atual é de R$ {saldo:.2f}")
        except ValueError:
                print("Por favor, insira um número válido.")

    if opcao == "4":
        print("Obrigado por utilizar o Banco Python!")
        import sys
        # Para sair do programa
        sys.exit()

menu_inicial()
