# PredictionResult
Scraping data  and getting the prediction result


from selenium import  webdriver
import requests
from selenium.webdriver.common.by import By
import os
storeSmileIntoList = []
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import pandas as pd
import glob
import csv
storing_Smile = {}
options = webdriver.ChromeOptions()
preferences = {"download.default_directory": f"{os.getcwd()}\Prediction Elements"}
options.add_experimental_option("prefs", preferences)
driver = webdriver.Chrome(options=options)
def opening_Csv():
    with open('Wurfbainia_villosa.csv') as csvfile:
        smiles = csv.DictReader(csvfile)
        #this loop will read the second column from dic to append it into LIST
        for key in smiles:
            storeSmileIntoList.append(key['SMILES'])
    try:
        directoryName = os.path.expandvars = 'Prediction Elements'
        path = os.makedirs(directoryName)
    except:
        pass
opening_Csv()


for countSmileList in range(96,len(storeSmileIntoList)):
    try:

        driver.get('http://www.swisstargetprediction.ch/')
        driver.find_element(By.XPATH, '//input[@id="smilesBox"]').send_keys(storeSmileIntoList[countSmileList])
        WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.XPATH, '//input[@id="submitButton"]'))).click()
        driver.find_element(By.XPATH,'//button[@class="dt-button buttons-csv buttons-html5"]').click()
        print(storeSmileIntoList[countSmileList])
        checkingDirectory = f"{os.getcwd()}\Prediction Elements"
    except:
        pass
