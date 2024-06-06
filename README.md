import math 
import sympy as sp
import pandas as pd
import matplotlib.pyplot as plt
import scipy.integrate as integrate
import numpy as np
from tkinter import *
from tkinter import ttk
from tkinter import messagebox

# Funções para operações básicas
def soma(a, b):
    return a + b

def subtracao(a, b):
    return a - b

def multiplicacao(a, b):
    return a * b

def divisao(a, b):
    if b == 0:
        messagebox.showerror("Erro", "Divisão por zero!")
        return None
    else:
        return a / b

# Funções para potenciação e radiciação
def potenciacao(a, n):
    return a ** n

def raiz_quadrada(a):
    if a < 0:
        messagebox.showerror("Erro", "Raiz quadrada de número negativo!")
        return None
    else:
        return a ** 0.5

def raiz_n_esima(a, n):
    if a < 0 and n % 2 == 0:
        messagebox.showerror("Erro", "Raiz n-ésima complexa!")
        return None
    else:
        return a ** (1 / n)

# Funções para funções matemáticas
def seno(x):
    return math.sin(x)

def cosseno(x):
    return math.cos(x)

def tangente(x):
    if math.cos(x) == 0:
        messagebox.showerror("Erro", "Tangente indefinida!")
        return None
    else:
        return math.tan(x)

def logaritmo_natural(x):
    if x <= 0:
        messagebox.showerror("Erro", "Logaritmo natural de número não positivo!")
        return None
    else:
        return math.log(x)

def logaritmo_decimal(x):
    if x <= 0:
        messagebox.showerror("Erro", "Logaritmo decimal de número não positivo!")
        return None
    else:
        return math.log10(x)

# Funções para operações com memória
memoria = {}

def adicionar_memoria(nome, valor):
    memoria[nome] = valor

def remover_memoria(nome):
    if nome in memoria:
        del memoria[nome]
    else:
        messagebox.showinfo("Informação", f"Nome '{nome}' não encontrado na memória.")

def consultar_memoria(nome):
    if nome in memoria:
        return memoria[nome]
    else:
        messagebox.showinfo("Informação", f"Nome '{nome}' não encontrado na memória.")

def limpar_memoria():
    memoria.clear()
    messagebox.showinfo("Informação", "Memória limpa.")

# Funções para integração numérica
def integral_numerica(funcao_str, a, b, n):
    try:
        # Converter a função string em função Python
        funcao = eval("lambda x: " + funcao_str)
        resultado, _ = integrate.quad(funcao, a, b, epsabs=1e-5, limit=n)
        return resultado
    except Exception as e:
        messagebox.showerror("Erro", f"Erro ao avaliar a função: {e}")
        return None

# Funções para derivada numérica
def derivada_numerica(funcao_str, x, h):
    try:
        # Converter a função string em função Python
        funcao = eval("lambda x: " + funcao_str)
        derivada = (funcao(x + h) - funcao(x - h)) / (2 * h)
        return derivada
    except Exception as e:
        messagebox.showerror("Erro", f"Erro ao avaliar a função: {e}")
        return None

# Funções para transformada de Fourier
def transformada_fourier(sinal):
    fourier = np.fft.fft(sinal)
    return fourier

# Interface gráfica (utilizando tkinter como exemplo)
def interface():
    # Criar a janela principal
    janela = Tk()
    janela.title("Calculadora Científica Avançada - Engenharia Civil e Básica")

    # Abas para separação das funcionalidades
    abas = ttk.Notebook(janela)
    aba_basica = ttk.Frame(abas)
    aba_avancada = ttk.Frame(abas)
    aba_engenharia_civil = ttk.Frame(abas)
    abas.add(aba_basica, text="Básica")
    abas.add(aba_avancada, text="Avançada")
    abas.add(aba_engenharia_civil, text="Eng. Civil")
    abas.pack(expand=True, fill="both")

    # Funcionalidades básicas (utilizar widgets do tkinter)
    def soma_interface():
        try:
            a = float(entrada_a_soma.get())
            b = float(entrada_b_soma.get())
            resultado = soma(a, b)
            label_resultado_soma.config(text=f"Resultado: {resultado}")
        except ValueError:
            messagebox.showerror("Erro", "Entrada inválida!")

    label_a_soma = Label(aba_basica, text="Valor de a:")
    label_a_soma.pack()
    entrada_a_soma = Entry(aba_basica)
    entrada_a_soma.pack()

    label_b_soma = Label(aba_basica, text="Valor de b:")
    label_b_soma.pack()
    entrada_b_soma = Entry(aba_basica)
    entrada_b_soma.pack()

    botao_somar = Button(aba_basica, text="Somar", command=soma_interface)
    botao_somar.pack()

    label_resultado_soma = Label(aba_basica, text="Resultado:")
    label_resultado_soma.pack()

    def subtracao_interface():
        try:
            a = float(entrada_a_subtracao.get())
            b = float(entrada_b_subtracao.get())
            resultado = subtracao(a, b)
            label_resultado_subtracao.config(text=f"Resultado: {resultado}")
        except ValueError:
            messagebox.showerror("Erro", "Entrada inválida!")

    label_a_subtracao = Label(aba_basica, text="Valor de a:")
    label_a_subtracao.pack()
    entrada_a_subtracao = Entry(aba_basica)
    entrada_a_subtracao.pack()

    label_b_subtracao = Label(aba_basica, text="Valor de b:")
    label_b_subtracao.pack()
    entrada_b_subtracao = Entry(aba_basica)
    entrada_b_subtracao.pack()

    botao_subtrair = Button(aba_basica, text="Subtrair", command=subtracao_interface)
    botao_subtrair.pack()

    label_resultado_subtracao = Label(aba_basica, text="Resultado:")
    label_resultado_subtracao.pack()

    def multiplicacao_interface():
        try:
            a = float(entrada_a_multiplicacao.get())
            b = float(entrada_b_multiplicacao.get())
            resultado = multiplicacao(a, b)
            label_resultado_multiplicacao.config(text=f"Resultado: {resultado}")
        except ValueError:
            messagebox.showerror("Erro", "Entrada inválida!")

    label_a_multiplicacao = Label(aba_basica, text="Valor de a:")
    label_a_multiplicacao.pack()
    entrada_a_multiplicacao = Entry(aba_basica)
    entrada_a_multiplicacao.pack()

    label_b_multiplicacao = Label(aba_basica, text="Valor de b:")
    label_b_multiplicacao.pack()
    entrada_b_multiplicacao = Entry(aba_basica)
    entrada_b_multiplicacao.pack()

    botao_multiplicar = Button(aba_basica, text="Multiplicar", command=multiplicacao_interface)
    botao_multiplicar.pack()

    label_resultado_multiplicacao = Label(aba_basica, text="Resultado:")
    label_resultado_multiplicacao.pack()

    def divisao_interface():
        try:
            a = float(entrada_a_divisao.get())
            b = float(entrada_b_divisao.get())
            resultado = divisao(a, b)
            if resultado is not None:
                label_resultado_divisao.config(text=f"Resultado: {resultado}")
        except ValueError:
            messagebox.showerror("Erro", "Entrada inválida!")

    label_a_divisao = Label(aba_basica, text="Valor de a:")
    label_a_divisao.pack()
    entrada_a_divisao = Entry(aba_basica)
    entrada_a_divisao.pack()

    label_b_divisao = Label(aba_basica, text="Valor de b:")
    label_b_divisao.pack()
    entrada_b_divisao = Entry(aba_basica)
    entrada_b_divisao.pack()

    botao_dividir = Button(aba_basica, text="Dividir", command=divisao_interface)
    botao_dividir.pack()

    label_resultado_divisao = Label(aba_basica, text="Resultado:")
    label_resultado_divisao.pack()

    # Funcionalidades avançadas (integração, derivada, transformada de Fourier)
    def integracao_numerica():
        funcao_str = entrada_funcao.get()
        a = float(entrada_limite_a.get())
        b = float(entrada_limite_b.get())
        n = int(entrada_pontos.get())
        resultado = integral_numerica(funcao_str, a, b, n)
        if resultado is not None:
            label_resultado_integral.config(text=f"Resultado: {resultado}")

    label_funcao = Label(aba_avancada, text="Função (em Python):")
    label_funcao.pack()
    entrada_funcao = Entry(aba_avancada)
    entrada_funcao.pack()

    label_limite_a = Label(aba_avancada, text="Limite inferior:")
    label_limite_a.pack()
    entrada_limite_a = Entry(aba_avancada)
    entrada_limite_a.pack()

    label_limite_b = Label(aba_avancada, text="Limite superior:")
    label_limite_b.pack()
    entrada_limite_b = Entry(aba_avancada)
    entrada_limite_b.pack()

    label_pontos = Label(aba_avancada, text="Número de pontos:")
    label_pontos.pack()
    entrada_pontos = Entry(aba_avancada)
    entrada_pontos.pack()

    botao_integrar = Button(aba_avancada, text="Calcular Integral", command=integracao_numerica)
    botao_integrar.pack()

    label_resultado_integral = Label(aba_avancada, text="Resultado:")
    label_resultado_integral.pack()

    def derivada_numerica_interface():
        funcao_str = entrada_funcao_derivada.get()
        x = float(entrada_ponto_x.get())
        h = float(entrada_passo_h.get())
        resultado = derivada_numerica(funcao_str, x, h)
        if resultado is not None:
            label_resultado_derivada.config(text=f"Resultado: {resultado}")

    label_funcao_derivada = Label(aba_avancada, text="Função (em Python):")
    label_funcao_derivada.pack()
    entrada_funcao_derivada = Entry(aba_avancada)
    entrada_funcao_derivada.pack()

    label_ponto_x = Label(aba_avancada, text="Ponto x:")
    label_ponto_x.pack()
    entrada_ponto_x = Entry(aba_avancada)
    entrada_ponto_x.pack()

    label_passo_h = Label(aba_avancada, text="Passo h:")
    label_passo_h.pack()
    entrada_passo_h = Entry(aba_avancada)
    entrada_passo_h.pack()

    botao_derivar = Button(aba_avancada, text="Calcular Derivada", command=derivada_numerica_interface)
    botao_derivar.pack()

    label_resultado_derivada = Label(aba_avancada, text="Resultado:")
    label_resultado_derivada.pack()

    def transformada_fourier_interface():
        sinal_str = entrada_sinal_fourier.get()
        try:
            sinal = eval(sinal_str)
            if isinstance(sinal, list):
                resultado = transformada_fourier(sinal)
                label_resultado_fourier.config(text=f"Resultado: {resultado}")
            else:
                messagebox.showerror("Erro", "O sinal deve ser uma lista.")
        except Exception as e:
            messagebox.showerror("Erro", f"Erro ao avaliar o sinal: {e}")

    label_sinal_fourier = Label(aba_avancada, text="Sinal (lista):")
    label_sinal_fourier.pack()
    entrada_sinal_fourier = Entry(aba_avancada)
    entrada_sinal_fourier.pack()

    botao_fourier = Button(aba_avancada, text="Calcular Fourier", command=transformada_fourier_interface)
    botao_fourier.pack()

    label_resultado_fourier = Label(aba_avancada, text="Resultado:")
    label_resultado_fourier.pack()

    # Adicionar mais funcionalidades para a aba de engenharia civil conforme necessário

    janela.mainloop()

# Executar a interface
interface()
