import tkinter as tk
from tkinter import ttk
from tkinter import messagebox as mb
import psycopg2
import datetime

conexao = psycopg2.connect(
    user="postgres",
    password="postgre",
    host="localhost",
    port="5432",
    database="RAD"
)

cursor = conexao.cursor()

def inserir_paciente():
    try:
        cpf_val = cpf.get()
        nome_val = nome.get().upper()
        sexo_val = sexo.get().upper
        dtnasc_val = dtnasc.get()
        telefone_val = telefone.get()
        cursor.execute("insert into cliente values(%s, %s, %s, %s, %s)", (cpf_val, nome_val, sexo_val, dtnasc_val, telefone_val))
        conexao.commit()

        cpf.delete(0, tk.END)
        nome.delete(0, tk.END)
    
        dtnasc.delete(0, tk.END)
        telefone.delete(0, tk.END)
        mb.showinfo(title="Paciente Cadastrado", message="Paciente cadastrado com sucesso!")
    
    except Exception as e:
        conexao.rollback()
        mb.showerror(title="Cadastro não efetuado", message=f"Verifique os dados! \nErro: {str(e)}")

def alterar_paciente():
    try:
        cpf_val = cpf.get()
        nome_val = nome.get().upper()
        sexo_val = sexo.get().upper()
        dtnasc_val = dtnasc.get()
        telefone_val = telefone.get()
        cursor.execute("update cliente set cpf=%s, nome=%s, sexo=%s, dtnasc=%s, telefone=%s where cpf=%s", (cpf_val, nome_val, sexo_val, dtnasc_val, telefone_val, cpf_val))
        conexao.commit()

        cpf.delete(0, tk.END)
        nome.delete(0, tk.END)
    
        dtnasc.delete(0, tk.END)
        telefone.delete(0, tk.END)
        mb.showinfo(title="Paciente Alterado", message="Paciente alterado com sucesso!")
    
    except Exception as e:
        conexao.rollback()
        mb.showerror(title="Alteração não efetuada", message=f"Verifique os dados! \nErro: {str(e)}")




janela = tk.Tk()
janela.title('Pré-consulta - Triagem')
'''janela.config(bg='lightblue')'''

#Cadastro

cadastro = ttk.Labelframe(janela, text="Cadastar Paciente", padding=(10,10))
cadastro.grid(column= 0, row= 0, columnspan=3, padx=5, pady=5, sticky="nsew")

consulta = ttk.Labelframe(janela, text="Cadastar Pré-Consulta (Triagem)", padding=(10,10))
consulta.grid(column= 0, row= 9, columnspan=3, padx=5, pady=5, sticky="nsew")

visualizar = ttk.Labelframe(janela, text="Visualizar Pré-Consulta (Triagem)", padding=(10,10))
visualizar.grid(column= 4, row= 9, columnspan=3, padx=5, pady=5, sticky="nsew")

ttk.Label(cadastro, text = "Cadastro de paciente:").grid(column=0, row=0)

ttk.Label(cadastro, text = "CPF:").grid(column=0, row=1, sticky="e")
cpf = tk.Entry(cadastro)
cpf.grid(column=1, row=1)

ttk.Label(cadastro, text = "Nome:").grid(column=0, row=2, sticky="e")
nome = tk.Entry(cadastro)
nome.grid(column=1, row=2,)

ttk.Label(cadastro, text = "Sexo:").grid(column=0, row=3, sticky="e")
sexo = tk.StringVar()
tk.Radiobutton(cadastro, text="Masculino", padx=15, variable = sexo, value= "Masculino").grid(column=1, row=3)
tk.Radiobutton(cadastro, text="Feminino", padx=15, variable = sexo, value= "Feminino").grid(column=2, row=3)


ttk.Label(cadastro, text = "Data de Nascim.:").grid(column=0, row=4, sticky="e")
dtnasc = tk.Entry(cadastro)
dtnasc.grid(column=1, row=4)

ttk.Label(cadastro, text = "Telefone:").grid(column=0, row=5, sticky="e")
telefone = tk.Entry(cadastro)
telefone.grid(column=1, row=5)

ttk.Label(cadastro, text = " ").grid(column=0, row=6, sticky="e")

tk.Button(cadastro, text="Inserir Paciente", width=18, command=inserir_paciente).grid(column=1, row=7)
tk.Button(cadastro, text="Alterar Paciente", width=18, command=alterar_paciente).grid(column=2, row=7)

ttk.Label(cadastro, text = " ").grid(column=0, row=8, sticky="e")

#Pré-Consulta (Triagem)

ttk.Label(consulta, text="CPF Paciente:").grid(column=0, row=10)
cpf_consulta = tk.Entry(consulta)
cpf_consulta.grid(column=1, row=10)

def limpar_entry(cpf_consulta):
    cpf_consulta.delete(0, tk.END)

def carregar_dados():
    
    for widget in dados_paciente.winfo_children():
        widget.destroy()

    cpf_consulta_f = cpf_consulta.get()
    cursor.execute("select cpf, nome, sexo, dtnasc, telefone from cliente where cpf = %s", (cpf_consulta_f,))
    resultados = cursor.fetchone()

    if resultados:
        cpf, nome, sexo, dtnasc, telefone = map(str, resultados)
        dtnasc_formatada = datetime.datetime.strptime(dtnasc, '%Y-%m-%d').strftime('%d/%m/%Y')
        ttk.Label(dados_paciente, foreground="darkred", text= f"{cpf}").grid(column=1, columnspan=2, row=12, sticky="w")
        ttk.Label(dados_paciente, foreground="darkred", text= f"{nome}").grid(column=1, columnspan=2, row=13, sticky="w")
        ttk.Label(dados_paciente, foreground="darkred", text= f"{sexo}").grid(column=1, columnspan=2, row=14, sticky="w")
        ttk.Label(dados_paciente, foreground="darkred", text= f"{dtnasc_formatada}").grid(column=1, columnspan=2, row=15, sticky="w")
        ttk.Label(dados_paciente, foreground="darkred", text= f"{telefone}").grid(column=1, columnspan=2, row=16, sticky="w")
        tk.Label(dados_paciente, text= "CPF:").grid(column=0, row=12, sticky="e")
        tk.Label(dados_paciente, text= "Sexo:").grid(column=0, row=14, sticky="e")
        tk.Label(dados_paciente, text= "Nome:").grid(column=0, row=13, sticky="e")
        tk.Label(dados_paciente, text= "Data Nasc.:").grid(column=0, row=15, sticky="e")
        tk.Label(dados_paciente, text= "Telefone:").grid(column=0, row=16, sticky="e")
    
    else:
        limpar_entry(cpf_consulta)
        tk.Label(dados_paciente, text= "CPF:").grid(column=0, row=12, sticky="e")
        tk.Label(dados_paciente, text= "Sexo:").grid(column=0, row=14, sticky="e")
        tk.Label(dados_paciente, text= "Nome:").grid(column=0, row=13, sticky="e")
        tk.Label(dados_paciente, text= "Data Nasc.:").grid(column=0, row=15, sticky="e")
        tk.Label(dados_paciente, text= "Telefone:").grid(column=0, row=16, sticky="e")
        mb.showerror("Atenção", "Paciente não encontrado!")
              

tk.Button(consulta, text="Consultar Paciente", width=18, command=carregar_dados).grid(column=3, row=10, sticky="nsew")

dados_paciente = ttk.LabelFrame(consulta, text="Dados do paciente:", padding=(2,2))
dados_paciente.grid(column= 0, row= 11, columnspan=3, padx=2, pady=2, sticky="nsew")

tk.Label(dados_paciente, text= "CPF:").grid(column=0, row=12, sticky="e")
tk.Label(dados_paciente, text= "Sexo:").grid(column=0, row=14, sticky="e")
tk.Label(dados_paciente, text= "Nome:").grid(column=0, row=13, sticky="e")
tk.Label(dados_paciente, text= "Data Nasc.:").grid(column=0, row=15, sticky="e")
tk.Label(dados_paciente, text= "Telefone:").grid(column=0, row=16, sticky="e")

ttk.Label(consulta, text = " ").grid(column=0, row=17, sticky="e")

novo = tk.StringVar()

tk.Label(consulta, text="Primeira consulta nesta unidade?").grid(column=0, row=18, sticky="e")
tk.Radiobutton(consulta, text="Sim", padx=15, variable = novo, value= "sim").grid(column=1, row=18)
tk.Radiobutton(consulta, text="Não", padx=15, variable = novo, value= "nao").grid(column=2, row=18)

ttk.Label(consulta, text = " ").grid(column=0, row=19, sticky="e")

hanseniase = tk.StringVar()
hepatite = tk.StringVar()
hiv = tk.StringVar()
meningite = tk.StringVar()
sifilis = tk.StringVar()
outras = tk.StringVar()

tk.Label(consulta, text="Motivo da Visita:").grid(column=0, row=20, sticky="e")
ttk.Checkbutton(consulta, text= "Hanseníase", variable=hanseniase, onvalue="Hanseníase", offvalue="").grid(column=1, row=20, sticky="w")
ttk.Checkbutton(consulta, text= "Hepatite", variable=hepatite, onvalue="Hepatite", offvalue="").grid(column=2, row=20, sticky="w")
ttk.Checkbutton(consulta, text= "HIV", variable=hiv, onvalue="HIV", offvalue="").grid(column=1, row=21, sticky="w")
ttk.Checkbutton(consulta, text= "Meningite", variable=meningite, onvalue="Meningite", offvalue="").grid(column=2, row=21, sticky="w")
ttk.Checkbutton(consulta, text= "Sífilis", variable=sifilis, onvalue="Sífilis", offvalue="").grid(column=1, row=22, sticky="w")
ttk.Checkbutton(consulta, text= "Outras", variable=outras, onvalue="Outras", offvalue="").grid(column=2, row=22, sticky="w")

ttk.Label(consulta, text = " ").grid(column=0, row=23, sticky="e")

tratamento = tk.StringVar()

tk.Label(consulta, text="Ja fez ou está em tratamento?").grid(column=0, row=24, sticky="e")
tk.Radiobutton(consulta, text="Sim", padx=15, variable = tratamento, value= "sim").grid(column=1, row=24)
tk.Radiobutton(consulta, text="Não", padx=15, variable = tratamento, value= "nao").grid(column=2, row=24)

def gerar_consulta():
    try:

        cpf_consulta_db = cpf_consulta.get()
        novo_db = novo.get()
        hanseniase_db = hanseniase.get()
        hepatite_db = hepatite.get()
        hiv_db = hiv.get()
        meningite_db = meningite.get()
        sifilis_db = sifilis.get()
        outras_db = outras.get()
        tratamento_db = tratamento.get()
        data = datetime.datetime.now()
        data_db = data.date()

        cursor.execute( "insert into triagem values(%s, %s, %s,%s, %s, %s, %s, %s, %s, %s)", (cpf_consulta_db, data_db, novo_db, hanseniase_db, hepatite_db, hiv_db, meningite_db, sifilis_db, outras_db, tratamento_db))
        conexao.commit()
        mb.showinfo(title="Pré-Consulta Gerada", message="Pré-consulta GERADA com sucesso!")

    except Exception as e:
        conexao.rollback()
        mb.showerror(title="Pré-Consulta Negada", message=f"Pré-consulta negada! Corrija os dados! \nErro: {str(e)}")

def alterar_consulta():
    try:

        cpf_consulta_db = cpf_consulta.get()
        novo_db = novo.get()
        hanseniase_db = hanseniase.get()
        hepatite_db = hepatite.get()
        hiv_db = hiv.get()
        meningite_db = meningite.get()
        sifilis_db = sifilis.get()
        outras_db = outras.get()
        tratamento_db = tratamento.get()
        data = datetime.datetime.now()
        data_db = data.date()

        cursor.execute( "update triagem set cpf=%s, data=%s, novo=%s, hanseniase=%s, hepatite=%s, hiv=%s, meningite=%s, sifilis=%s, outras=%s, tratamento=%s where cpf=%s", (cpf_consulta_db, data_db, novo_db, hanseniase_db, hepatite_db, hiv_db, meningite_db, sifilis_db, outras_db, tratamento_db, cpf_consulta_db))
        conexao.commit()
        mb.showinfo(title="Pré-Consulta Alterada", message="Pré-consulta ALTERADA com sucesso!")

    except Exception as e:
        conexao.rollback()
        mb.showerror(title="Alteração de Pré-Consulta Negada", message=f"Alteração de Pré-consulta negada! Corrija os dados! \nErro: {str(e)}")

def deletar_consulta():
    try:

        cpf_consulta_db = cpf_consulta.get()
        data = datetime.datetime.now()
        data_db = data.date()

        cursor.execute( "delete from triagem where cpf=%s and data=%s", (cpf_consulta_db, data_db))
        conexao.commit()
        mb.showwarning(title="Pré-Consulta Deletada", message="Pré-consulta EXCLUIDA com sucesso!")

    except Exception as e:
        conexao.rollback()
        mb.showerror(title="Deleção de Pré-Consulta Negada", message=f"Exclusão de Pré-consulta negada! Corrija os dados! \nErro: {str(e)}")

tk.Label(consulta, text=" ").grid(column=0, row=25, sticky="e")

tk.Button(consulta, text="Imprimir Pré-Consulta", width=18, command=gerar_consulta).grid(column=1, row=26, sticky="nsew")
tk.Button(consulta, text="Alterar Pré-Consulta", width=18, command=alterar_consulta).grid(column=2, row=26, sticky="nsew")
tk.Button(consulta, text="Excluir Pré-Consulta", width=18, command=deletar_consulta).grid(column=3, row=26, sticky="nsew")

#Visualizar

tk.Label(visualizar, text="CPF:").grid(column=4, row=9, sticky="e")
cpf_vis = tk.Entry(visualizar)
cpf_vis.grid(column=5, row=9)

tk.Label(visualizar, text="Data:").grid(column=4, row=10, sticky="e")
data_vis = tk.Entry(visualizar)
data_vis.grid(column=5, row=10)

def visualizar_consulta():
    try:
        cpf_vis_f = cpf_vis.get()
        data_vis_f = data_vis.get()

        cursor.execute("select nome from cliente where cpf=%s", (cpf_vis_f,))
        nome_pac = cursor.fetchone()

        cursor.execute("select cpf, data, novo, hanseniase, hepatite, hiv, meningite, sifilis, outras, tratamento from triagem where cpf=%s and data=%s", (cpf_vis_f, data_vis_f))
        dados_consulta = cursor.fetchone()

        
        cpf, data, novo, hanseniase, hepatite, hiv, meningite, sifilis, outras, tratamento = map(str, dados_consulta)
        dt_formatada = datetime.datetime.strptime(data, '%Y-%m-%d').strftime('%d/%m/%Y')

        ttk.Label(visualizar, foreground="darkgreen", text= f"Nome: {nome_pac[0]}\nCPF: {cpf}\n\nData: {dt_formatada}\n\nPaciente novo? {novo}\n\nDoenças:\n{hanseniase}\n{hepatite}\n{hiv}\n{meningite}\n{sifilis}\n{outras}\n\nPaciente em tratamento? {tratamento}").grid(column=5, columnspan=2, row=12, sticky="w")
                
    except Exception as e:
        mb.showerror(title="Visualização de préconsulta", message=f"Nenhuma pré-consulta (triagem) cadastrada para esse paciente nesta data! \nErro: {str(e)}")


tk.Button(visualizar, text="Visualizar Pré-Consulta", width=18, command=visualizar_consulta).grid(column=5, row=11, sticky="nsew")

janela.mainloop()
cursor.close()
conexao.close()
