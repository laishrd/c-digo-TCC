# código-TCC
Código referente ao Trabalho de Conclusão de Curso de Engenharia de Sistemas.

#Instruções:  
  1. É necessário adicionar um arquivo "hif_vegetation_dataset.h5", na pasta "data", para que o código funcione.
  2. Deixei um arquivo .db já pronto, se quiser que o código gere um é só apagar esse que deixei.

#Estrutura:
```
codigo_TCC/
├── data/
│   ├── hif_vegetation_dataset.h5  # HDF5 existente
│   └── hif_vegetation_data.db     # Banco de dados SQLite criado após execução etl_metadata.py
├── script/
│   └── etl_metadata.py            # Cria o banco de dados e popula ele com dados extraídos do arquivo HDF5
└── README.md                      # Documentação
```


#Base de dados hibrida:
    As waveforms são dados muito grandes, por exemplo, para um teste podemos ter 400mil linhas em apenas um parametro (como voltage_hf). Se eu colocasse isso diretamente no banco de dados, ele seria muito pesado também e pouco funcional. 
    Então, os metadados estão em SQL e as waveforms no arquivo HDF5. O que faz a ligação entre eles é o atributo hdf5_path. Com essa abordagem hibrida as consultas ficam mais rápidas e eficientes, porque a ideia é que só sejam carregados dados bruto (formas de onda) quando necessário e apenas o necessário porque com as consultas SQL já saberemos exatamente qual testes queremos ter acesso. Sem precisar carregar tudo como é feito atualmente.


