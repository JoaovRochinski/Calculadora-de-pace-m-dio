import streamlit as st

def calcula_pace(minutos, distancia, unidade):
    try:
        assert minutos > 0 and distancia > 0

        # Calcula segundos por unidade
        total_segundos = minutos * 60
        segundos_por_unidade = total_segundos / distancia

        # Converte os segundos para minutos e segundos
        minutos_por_unidade = int(segundos_por_unidade // 60)
        segundos_restantes = int(segundos_por_unidade % 60)

        # Formata o ritmo médio (pace) como "minutos:segundos"
        pace = f"{minutos_por_unidade}:{segundos_restantes:02d}"  # Adiciona zero à esquerda se necessário
        return f"O ritmo médio é de {pace} por {unidade}."
    except AssertionError:
        return "Os valores devem ser positivos."
    except Exception as e:
        return f"Ocorreu um erro: {str(e)}"

# Interface do Streamlit
st.title("Calculadora de Pace")

# Solicita ao usuário o tempo total em minutos
minutos = st.number_input("Digite o tempo total em minutos:", min_value=0.01, format="%.2f")

# Pergunta se quer calcular em quilômetros (K) ou milhas (M)
unidade = st.selectbox("Você quer calcular em:", ("quilômetros", "milhas"))

# Solicita a distância percorrida de acordo com a unidade escolhida
if unidade == "quilômetros":
    distancia = st.number_input("Digite a distância percorrida em quilômetros:", min_value=0.01, format="%.2f")
    unidade_display = "quilômetros"
else:
    distancia = st.number_input("Digite a distância percorrida em milhas:", min_value=0.01, format="%.2f")
    unidade_display = "milhas"

# Botão para calcular
if st.button("Calcular Pace"):
    resultado = calcula_pace(minutos, distancia, unidade_display)
    st.success(resultado)
