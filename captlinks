import pandas as pd
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
import time

# Ler a planilha com os SKUs
df_skus = pd.read_csv("skus.csv", sep=";", index_col=False, low_memory=False)

# Configuração do Selenium e do WebDriver (neste caso, o Chrome)
driver = webdriver.Chrome()
driver.get("")  # Insira a URL do site desejado

# Lista para armazenar os links das páginas
links_paginas = []

# Realizar a busca para cada SKU na planilha
for sku in df_skus['skus']:
    # Encontrar o campo de busca e enviar o SKU
    time.sleep(4)
    campo_busca = driver.find_element(By.XPATH, '')# Insira o ID do elemento desejado
    campo_busca.clear()  # Limpar o campo de busca
    campo_busca.send_keys(sku)  # Enviar o SKU
    campo_busca.send_keys(Keys.RETURN)  # Pressionar a tecla Enter
    
    # Capturar o link da página de resultado
    link_pagina = driver.current_url
    links_paginas.append(link_pagina)

# Criar um DataFrame com os links das páginas
df_links = pd.DataFrame({"SKU": df_skus['skus'], "Link": links_paginas})

# Salvar os links em um arquivo Excel
df_links.to_excel("links_paginas.xlsx", index=False)

# Fechar o WebDriver
driver.quit()
