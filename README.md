- **Cross-Attention**  
  \[
    v_{i+1} \;=\; \mathrm{Attention}\bigl(Q = v_i,\;K = \tau_{\theta}(y),\;V = \tau_{\theta}(y)\bigr)
    \quad(\text{3–4 layers})
  \]

- **Diffusion Loss**  
  \[
    \mathcal{L}(v) \;=\; \mathbb{E}_{z_t,y,t}\Bigl\|\epsilon \;-\; \epsilon_{\theta}\bigl(z_t,\,t,\,v\bigr)\Bigr\|^2
  \]

- **Optimization**  
  Update only \(v\) over ∼1 K–2 K iterations (∼20 min on one GPU)
