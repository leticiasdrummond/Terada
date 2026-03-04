## EV-Scheduler: Otimização Multiobjetivo para Dimensionamento de Microrredes com Integração de Veículos Elétricos

Este projeto implementa um modelo de otimização multiobjetivo baseado em MILP (Mixed-Integer Linear Programming) para o dimensionamento de microrredes que integram Recursos Energéticos Distribuídos (DERs) renováveis e não renováveis, Sistemas de Armazenamento de Energia por Bateria (BESS), Geradores Térmicos (TG), Estações de Recarga de Veículos Elétricos (EVCS) e estratégias de Vehicle-to-Grid (V2G).

Confira o artigo original em: https://doi.org/10.1016/j.segan.2025.101773

---

### Visão Geral

O modelo proposto foca em três objetivos principais:

- **Econômico**: Minimizar os custos totais do sistema, reduzindo tanto o CAPEX (despesas de capital) quanto o OPEX (despesas operacionais), incluindo o custo do serviço V2G.
- **Operacional**: Reduzir o tempo ocioso dos veículos elétricos (EVs) por meio da otimização dos cronogramas de recarga e do uso eficiente das estações de recarga.
- **Ambiental**: Reduzir as emissões de gases de efeito estufa (GHG) aumentando a penetração de energia renovável e utilizando estrategicamente o armazenamento de energia e o V2G.

O modelo incorpora técnicas de linearização para reduzir a complexidade computacional — como evitar o uso excessivo de variáveis binárias na representação das operações de carga e descarga dos BESS e EVs.

---

### Metodologia

A estrutura de otimização consiste em:

- **Formulação MILP**: O problema é definido como a minimização da soma do CAPEX e do OPEX descontado ao longo do horizonte operacional. Está sujeito a restrições de balanço energético, limites de capacidade dos componentes (PV, BESS, TG, EVCS) e disponibilidade dos EVs.
- **Abordagem Multiobjetivo**: Os trade-offs entre custo, emissões de GHG e tempo ocioso dos EVs são analisados por meio de uma fronteira de Pareto. O compromisso ótimo é alcançado por meio do método Nash Bargaining Solution (NBS).
- **Integração de Contingências**: O modelo inclui cenários off-grid para simular falhas na rede e outros eventos de contingência, garantindo a resiliência do sistema por meio da operação coordenada dos BESS e do V2G.

---

### Estudo de Caso

O estudo de caso considera:

- Um horizonte operacional de 20 anos com taxa de crescimento anual de custos.
- Parâmetros operacionais detalhados (capacidade máxima de EDS, limites de exportação, demanda de pico, penalidades por curtailment, etc.).
- Dados técnicos e econômicos dos componentes (PV, BESS, TG, EVCS) com base em estudos de mercado.
- Múltiplos cenários de geração fotovoltaica e variações de demanda, incluindo eventos de contingência off-grid.

Para definições detalhadas de parâmetros e agendamento dos EVs, consulte as tabelas fornecidas na documentação original.

---

### Resultados e Conclusões

Principais descobertas da simulação:

- Um preço de serviço V2G de 0,06 USD/kWh incentiva efetivamente a participação dos proprietários de EVs, equilibrando os custos do operador.
- O aumento do tempo ocioso dos EVs pode reduzir a necessidade de infraestrutura adicional de recarga sem comprometer a confiabilidade do sistema.
- A redução das emissões de GHG exige maiores investimentos em energia renovável e armazenamento, impactando os custos totais do sistema.
- O equilíbrio multiobjetivo (Equilíbrio de Nash) resultou em uma configuração com custo total do sistema de 1,06 MUSD, emissões anuais de GHG de 9,91 toneladas de CO₂ e tempo médio ocioso dos EVs de 33,75 minutos.

Esses resultados demonstram a viabilidade do modelo para apoiar decisões estratégicas no planejamento de microrredes inteligentes e sustentáveis.

---

### Repositório e Reprodutibilidade

O código, os dados e os modelos utilizados neste estudo estão disponíveis neste repositório para facilitar a reprodutibilidade e pesquisas futuras.

As simulações foram executadas com o solver Gurobi 11.0.1, com uma tolerância de MIP de 10%, em uma máquina com processador Intel® Core™ i7-13700 e 16 GB de RAM.

---

### Instalação e Uso

**Requisitos**

- Python 3.7+
- Bibliotecas: NumPy, Pandas, Matplotlib, Gurobi (ou qualquer solver MILP compatível)
- Pacotes adicionais listados no arquivo `requirements.txt`

**Instruções de Instalação**

1. Clone o repositório:
   ```bash
   git clone https://github.com/TeradaZenichi/ev-scheduler.git
   cd ev-scheduler
   ```

2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure o solver MILP (por exemplo, Gurobi) conforme a documentação oficial.

4. Para executar a otimização e gerar os gráficos de resultados, execute:
   ```bash
   python linearmodel.py
   ```

---

### Contribuições

Contribuições, sugestões e relatos de bugs são bem-vindos! Por favor, abra uma issue ou envie um pull request.

---

### Licença

Este projeto está licenciado sob a Licença MIT.

########################################################################################################################################################
# EV-Scheduler: Multi-Objective Optimization for Microgrid Sizing with Electric Vehicle Integration

This project implements a multi-objective optimization model based on MILP (Mixed-Integer Linear Programming) for the sizing of microgrids integrating renewable and non-renewable Distributed Energy Resources (DERs), Battery Energy Storage Systems (BESS), Thermal Generators (TG), Electric Vehicle Charging Stations (EVCS), and Vehicle-to-Grid (V2G) strategies.

Please check the original paper on: <https://doi.org/10.1016/j.segan.2025.101773>

## Overview

The proposed model focuses on three main objectives:
- **Economic:** Minimize the overall system costs by reducing both CAPEX (capital expenditure) and OPEX (operational expenditure), including the cost of the V2G service.
- **Operational:** Reduce the idle time of electric vehicles (EVs) by optimizing charging schedules and efficient use of charging stations.
- **Environmental:** Lower greenhouse gas (GHG) emissions by enhancing renewable energy penetration and strategically utilizing energy storage and V2G.

The model incorporates linearization techniques to reduce computational complexity—such as avoiding excessive use of binary variables in representing charging and discharging operations of BESS and EVs.

## Methodology

The optimization framework consists of:
- **MILP Formulation:** The problem is defined as minimizing the sum of CAPEX and discounted OPEX over the operational horizon. It is subject to energy balance constraints, component capacity limits (PV, BESS, TG, EVCS), and EV availability.
- **Multi-Objective Approach:** Trade-offs between cost, GHG emissions, and EV idle time are analyzed using a Pareto frontier. The optimal trade-off is achieved through a Nash Bargaining Solution (NBS) method.
- **Contingency Integration:** The model includes off-grid scenarios to simulate grid outages and other contingency events, ensuring system resilience through coordinated operation of BESS and V2G.

## Test Case

The test case considers:
- A 20-year operational horizon with an annual cost growth rate.
- Detailed operational parameters (maximum EDS capacity, export limits, peak load demand, curtailment penalties, etc.).
- Technical and economic data for the components (PV, BESS, TG, EVCS) based on market studies.
- Multiple scenarios for PV generation and load demand variations, including off-grid contingency events.

For detailed parameter definitions and EV scheduling, please refer to the tables provided in the original documentation.

## Results and Conclusions

Key findings from the simulation include:
- A V2G service price of 0.06 USD/kWh effectively incentivizes EV owner participation while balancing the operator's costs.
- Increased EV idle time can reduce the need for additional charging infrastructure without compromising system reliability.
- Lowering GHG emissions requires higher investments in renewable energy and storage, impacting overall system costs.
- The multi-objective equilibrium (Nash Equilibrium) reached a configuration with a total system cost of 1.06 MUSD, annual GHG emissions of 9.91 tons CO₂, and an average EV idle time of 33.75 minutes.

These results demonstrate the model’s viability for supporting strategic decisions in planning smart, sustainable microgrids.

## Repository and Reproducibility

The code, data, and models used in this study are available in this repository to facilitate reproducibility and further research. Simulations were executed using the Gurobi 11.0.1 solver with a 10% MIP gap on a machine equipped with an Intel® Core™ i7-13700 processor and 16 GB RAM.

## Installation and Usage

### Requirements
- Python 3.7+
- Libraries: NumPy, Pandas, Matplotlib, Gurobi (or any compatible MILP solver)
- Additional packages as listed in the `requirements.txt` file

### Installation Instructions
1. Clone the repository:
   ```bash
   git clone https://github.com/TeradaZenichi/ev-scheduler.git
   cd ev-scheduler

2. Install the dependencies:
  ```bash
  pip install -r requirements.txt
```
3. Configure the MILP solver (e.g., Gurobi) according to its official documentation.
  
4. To run the optimization and generate the result graphs, simply execute:
```bash
python linearmodel.py
```

## Contributing

Contributions, suggestions, and bug reports are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).



