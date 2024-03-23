from decimal import Decimal, getcontext

def calcular_pi_gauss_legendre(n_iteracoes):
    getcontext().prec = n_iteracoes + 2  # Precisão definida em duas unidades a mais para garantir a precisão desejada
    a = Decimal(1)
    b = 1 / Decimal(2).sqrt()
    t = Decimal(1) / Decimal(4)
    p = Decimal(1)

    for _ in range(n_iteracoes):
        a_next = (a + b) / Decimal(2)
        b = (a * b).sqrt()
        t -= p * (a - a_next) * (a - a_next)
        a = a_next
        p *= 2

    return (a + b) ** 2 / (4 * t)

while True:
    try:
        n = int(input("Insira o número de iterações desejado para calcular Pi (ou digite 0 para sair): "))
        if n == 0:
            print("Saindo do programa...")
            break
        elif n < 0:
            print("Por favor, insira um número inteiro não negativo.")
            continue
        
        print("O valor de PI com", n, "iterações é:")
        print(calcular_pi_gauss_legendre(n))
        print()
    except ValueError:
        print("Por favor, insira um número inteiro válido ou 0 para sair.")
