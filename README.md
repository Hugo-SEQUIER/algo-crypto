
### 1. `get_top_500_tokens()`

Récupère les 500 premières cryptomonnaies par capitalisation boursière depuis l'API de CoinGecko.

### 2. `get_historical_prices(crypto_id: str, vs_currency: str = 'usd', days: int = 180) -> list`

Obtient les prix historiques quotidiens d'une cryptomonnaie spécifique sur une période de 180 jours.

### 3. `add_180_days_data(df_tokens)`

Ajoute les données de prix sur 180 jours pour chaque token dans le DataFrame des tokens.

### 4. `fill_missing_prices_with_mean(df)`

Remplace les valeurs manquantes dans les prix par la moyenne des prix disponibles pour chaque token.

### 5. `calculate_daily_returns(prices)`

Calcule les rendements quotidiens basés sur les prix historiques.

### 6. `calculate_volatility(daily_returns)`

Calcule la volatilité (écart-type) des rendements quotidiens.

### 7. `calculate_risk_reward(expected_return, volatility)`

Calcule le ratio Risk-Reward basé sur le rendement attendu et la volatilité.

### 8. `calculate_dynamic_target(market_cap)`

Détermine un objectif dynamique de rendement en fonction de la capitalisation boursière.

### 9. `add_risk_reward_column(df)`

Ajoute une colonne "Risk-Reward" calculée pour chaque token dans le DataFrame.

### 10. `clear_rows_with_keywords(df, keywords)`

Supprime les tokens dont le nom contient certains mots-clés indésirables.

### 11. `add_marketcap_rank(df)`

Ajoute une colonne indiquant le rang de chaque token en fonction de sa capitalisation boursière.

### 12. `calculate_momentum_score(df)`

Calcule un score de momentum basé sur les variations de prix sur 1 jour, 7 jours et 30 jours.

### 13. `calculate_token_score(df, investment=100, alpha=0.4, beta=0.3, gamma=0.3)`

Calcule un score global pour chaque token en intégrant le Risk-Reward, la capitalisation boursière, le momentum et le gain potentiel.

## Utilisation

Le script effectue les étapes suivantes :

1. **Récupération des données :**

   ```python
   df_tokens = get_top_500_tokens()
   df_tokens_with_180_days = add_180_days_data(df_tokens)
   ```

2. **Nettoyage des données :**

   ```python
   df_tokens_with_180_days = fill_missing_prices_with_mean(df_tokens_with_180_days)
   df_tokens_with_180_days.to_excel('top_500_tokens_with_180_days.xlsx', index=False)
   ```

3. **Calcul des métriques de risque et de performance :**

   ```python
   df_tokens_with_risk_reward = add_risk_reward_column(df_tokens_with_180_days)
   df_tokens_with_risk_reward.to_excel('top_500_tokens_with_risk_reward_180.xlsx', index=False)
   ```

4. **Filtrage des tokens indésirables :**

   ```python
   keywords_to_exclude = ['wrapped', 'usd', 'tether', 'usdt', 'bridged', 'staked', 'weth', 'wbtc', 'btc']
   df_cleaned = clear_rows_with_keywords(df_tokens_with_risk_reward, keywords_to_exclude)
   df_cleaned.to_excel('top_500_tokens_cleaned_180.xlsx', index=False)
   ```

5. **Classement et score final :**

   ```python
   df_ranked_tokens = add_marketcap_rank(df_cleaned)
   df_ranked_tokens = calculate_token_score(df_ranked_tokens)
   df_ranked_tokens.to_excel('top_500_tokens_ranked_by_score_180.xlsx', index=False)
   ```

## Résultats

Le script génère plusieurs fichiers Excel contenant les données traitées et analysées :

- `top_500_tokens_with_180_days.xlsx` : Contient les 500 tokens avec leurs prix sur 180 jours.
- `top_500_tokens_with_risk_reward_180.xlsx` : Ajoute la colonne Risk-Reward.
- `top_500_tokens_cleaned_180.xlsx` : Nettoie les tokens indésirables basés sur des mots-clés.
- `top_500_tokens_ranked_by_score_180.xlsx` : Classe les tokens en fonction de leur score global calculé.
