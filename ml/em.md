Algorithme Expectation - Maximisation

# Description
 - Modèle probabilisete
 - Algorithme itératif. La vraisemblace augmente à chaque itération E-M.
 - Deux phases:
   - Phase "Expectation" : Estimation des données inconnues à partir des données observées. 
   
L'espérance est égale à :

$$
\begin{matrix}
\mathbb{E}[L(x;\theta)] & = & \mathbb{E}[\sum_i \log p(x_i / \theta)] & \\
                        & = & \mathbb{E}[\sum_i \log ( \sum_k p(z_k, x_i/ \theta) )] & \ (marginalisation) \\
                        & = & \mathbb{E}[\sum_i \log ( \sum_k p(z_k, x_i/ \theta)  * \frac{p(z_k/ x_i, \theta_t)}{p(z_k/ x_i, \theta_t)})] & \\
                        & = & \mathbb{E}[\sum_i \log ( \sum_k p(z_k/ x_i, \theta_t))  * \frac{p(z_k, x_i/ \theta}{p(z_k/ x_i, \theta_t)})] & \\
                        & \ge & \mathbb{E}[\sum_i  \sum_k p(z_k/ x_i, \theta_t))  * \log (\frac{p(z_k, x_i/ \theta}{p(z_k/ x_i, \theta_t)})] & Inégalité\ de \ Jensen\\
                        & \ge & \underbrace{\mathbb{E}(\mathcal{L}(x;z;))}_{Q(\theta,\theta^c): espérance\ conditionnelle\  de\ la\ log-vraisemblance\ des\ données\ complètes} - \underbrace{...}_{Constante,\ ne\ dépend\ pas\ de\ \theta}& 
\end{matrix}
$$ 

Inégalité de Jensen : $\phi(\mathbb{E}[X]) \le \mathbb{E}[\phi(X)]$

On calcule donc :

$
Q(\theta; \theta^t) = \mathbb(E)[\mathcal{L}((x, z); \theta) / \theta^t]
$

   - Phase "Maximisation": Maximisation du maximum de (log-)vraisemblance $L(x;\theta) = \sum_i \log f(x_i, \theta)$. Trouver les paramètres $\theta^{t+1}$ qui maximise $L(x;\theta)$, c'est-à-dire:

$$
\theta^{r+1} = \argmax_{\theta} Q(\theta,\theta^r)
$$

Si on maximise Q, on maximise aussi le maximum de log-vraisemblance

# Algorithme EM pour le Modèle de mélange gaussien

 - Ensemble de k-distributions de probabilités représentant k-clusters
 - Somme de plusieurs gaussiennes
 - **Objectif**: déterminer la moyenne $\mu_i$ et $\sigma_i$ de chaque gaussienne. On note $\theta_i = (\mu_i, \sigma_i)$
 - EM pour un mélange gaussien
   - Choix du nombre de classes k. $f \sim \mathcal{N}(\mu, \sigma)$
   - Initialisation des paramètres $\theta^0_k$
   - Calcul du log de vraisemblance: $\mathcal{L}(x, \theta^0_k) = \sum \log(\sum \alpha_k f(x_i, \theta^0_k))$ avec $\alpha_k$, la probabilité conditionnelle que $x_i \in \mathcal{C}_k$, sous contrainte que $\sum_k \alpha_k = 1$. coefficients de mélange
   - **Expectation**: calcul des probabilités d'appartenance$

   $$
   P(x_i \in C_k / x_i, \alpha_k, \theta_k) = \frac {\alpha^r_k f_k (x_i, \theta^r_k)} {\sum \alpha^r_j f_j (x_i, \theta^r_j)}
   $$

   - **Maximisation**: Calcul des $\theta$ et $\alpha$ qui maximisent le log-vraisemblance

   $$
   \alpha^{r+1}_k = \frac{1}{N} \sum P(x_i \in C_k / x_i, \alpha^r_i, \theta^r_i)
   $$

   $$
   \mu^{r+1}_k = \frac{\sum_i x_i P(x_i \in C_k / x_i, \alpha^r_i, \theta^r_i)}{\sum_i P(x_i \in C_k / x_i, \alpha^r_i, \theta^r_i)} 
   $$

   $$
   \sigma^{r+1}_k = \frac{\sum_i P(x_i \in C_k / x_i, \alpha^r_i, \theta^r_i) (x_i - \mu^{r+1}_k) (x_i - \mu^{r+1}_k)^t}{\sum_i P(x_i \in C_k / x_i, \alpha^r_i, \theta^r_i)} 
   $$