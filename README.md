# Sistema_bancario.md
Sistema bancário com Python

def depositar(saldo, valor, extrato):
    if valor > 0:
        saldo += valor
        extrato += f"Depósito: R$ {valor:.2f}\n"
        print("Depósito realizado com sucesso!")
    else:
        print("Valor inválido! O valor do depósito deve ser positivo.")
    
    return saldo, extrato

def sacar(saldo, valor, extrato, limite, numero_saques, limite_saques):
    excedeu_saldo = valor > saldo
    excedeu_limite = valor > limite
    excedeu_saques = numero_saques >= limite_saques

    if excedeu_saldo:
        print("Operação falhou! Você não tem saldo suficiente.")
    elif excedeu_limite:
        print("Operação falhou! O valor do saque excede o limite.")
    elif excedeu_saques:
        print("Operação falhou! Número máximo de saques diários excedido.")
    elif valor > 0:
        saldo -= valor
        extrato += f"Saque: R$ {valor:.2f}\n"
        numero_saques += 1
        print("Saque realizado com sucesso!")
    else:
        print("Operação falhou! O valor informado é inválido.")

    return saldo, extrato, numero_saques

def exibir_extrato(saldo, extrato, numero_saques):
    print("\n========== EXTRATO ==========")
    if not extrato:
        print("Nenhuma movimentação realizada.")
    else:
        print(extrato)
    
    print(f"\nSaldo atual: R$ {saldo:.2f}")
    print(f"Saques realizados hoje: {numero_saques}")
    print("=============================\n")

def menu():
    menu = """
    [1] Depósito
    [2] Saque
    [3] Extrato
    [4] Sair
    => """
    return input(menu)

def main():
    LIMITE_SAQUES = 3
    LIMITE = 500
    saldo = 0
    extrato = ""
    numero_saques = 0

    while True:
        opcao = menu()

        if opcao == "1":
            valor = float(input("Digite o valor do depósito: R$ "))
            saldo, extrato = depositar(saldo, valor, extrato)

        elif opcao == "2":
            valor = float(input("Digite o valor do saque: R$ "))
            saldo, extrato, numero_saques = sacar(
                saldo, valor, extrato, LIMITE, numero_saques, LIMITE_SAQUES
            )

        elif opcao == "3":
            exibir_extrato(saldo, extrato, numero_saques)

        elif opcao == "4":
            print("Obrigado por usar nosso sistema bancário. Volte sempre!")
            break
        
        else:
            print("Opção inválida! Por favor, selecione uma opção válida.")

if __name__ == "__main__":
    main()
