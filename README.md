# Stochastic Evasion Research Framework

Este repositório contém a implementação prática e o motor de simulação descritos na pesquisa **"Quantifying the Epistemological Limits of Distributed Anomaly Detection and Entropy Manipulation in Static Analysis"**.

## Visão Geral
Este framework formaliza a detecção de malwares como uma mudança de medida em espaços estocásticos. O objetivo principal é quantificar a degradação de telemetria em ambientes não estacionários (como pipelines CI/CD) e avaliar como a injeção de *drift* estocástico pode ser utilizada para contornar classificadores estatísticos.

## Componentes do Framework
O sistema é estruturado conforme o Funil de Quatro Camadas apresentado no artigo:
* **Layer 1 (Static):** Análise estrutural, layouts de seção e IAT.
* **Layer 2 (Runtime):** Telemetria de Syscalls e grafos de fluxo de controle.
* **Layer 3 (Latent):** Projeções de anomalia e redução de dimensionalidade.
* **Layer 4 (Topology):** Monitoramento de estado em topologias distribuídas.

## Implementação: Motor de Drift Estocástico
O núcleo da nossa metodologia de simulação de *drift* para ambientes de alta volatilidade (`drift_engine.py`):

```python
import numpy as np

def inject_stochastic_drift(X_baseline, time_step, drift_intensity=0.05):
    """
    Simula o desvio não estacionário em ambientes de CI/CD adicionando 
    deslocamento estocástico ao baseline de telemetria.
    """
    n_samples, n_features = X_baseline.shape
    
    # Simulação de movimento browniano para tradução de feature space
    # Adiciona displacement temporal para simular role drift
    drift_vector = np.random.normal(0, drift_intensity * np.sqrt(time_step), (n_samples, n_features))
    
    # Aplicação do deslocamento sistemático
    X_drifted = X_baseline + drift_vector
    return X_drifted
