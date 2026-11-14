import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# Konfigurasi Halaman
st.set_page_config(page_title="Visualisasi Fungsi Kuadrat", page_icon="📈", layout="centered")

st.title("📉 Visualisasi Perubahan Kurva Fungsi Kuadrat")
st.markdown("""
Aplikasi interaktif ini menunjukkan bagaimana perubahan nilai koefisien **$a$**, **$b$**, dan **$c$** 
pada fungsi kuadrat $f(x) = ax^2 + bx + c$ memengaruhi bentuk dan posisi kurva parabola.
""")

# Sidebar untuk pengaturan parameter
st.sidebar.header("Pengaturan Koefisien")
a = st.sidebar.slider("Koefisien a (Lebar & Arah Buka)", -5.0, 5.0, 1.0, 0.1)
if a == 0.0:
    a = 0.01  # Mencegah nilai 0 agar tetap berbentuk parabola

b = st.sidebar.slider("Koefisien b (Pergeseran Horizontal)", -10.0, 10.0, 0.0, 0.1)
c = st.sidebar.slider("Koefisien c (Titik Potong Sumbu Y)", -10.0, 10.0, 0.0, 0.1)

# Membuat rentang nilai X
x = np.linspace(-10, 10, 400)
y = a * x**2 + b * x + c

# Menghitung titik puncak (vertex)
vertex_x = -b / (2 * a)
vertex_y = a * vertex_x**2 + b * vertex_x + c

# Membuat Plot Matplotlib
fig, ax = plt.subplots(figsize=(8, 6))
ax.plot(x, y, label=f'$f(x) = {a}x^2 + {b}x + {c}$', color='#1f77b4', linewidth=3)
ax.axhline(0, color='black', linewidth=1.2, linestyle='--')
ax.axvline(0, color='black', linewidth=1.2, linestyle='--')

# Menandai titik puncak
ax.scatter([vertex_x], [vertex_y], color='red', s=80, zorder=5, 
           label=f'Puncak: ({vertex_x:.2f}, {vertex_y:.2f})')

# Pengaturan Batas Grafik dan Estetika
ax.set_xlim(-10, 10)
ax.set_ylim(-25, 25)
ax.set_xlabel('Sumbu X', fontsize=12)
ax.set_ylabel('Sumbu Y', fontsize=12)
ax.set_title('Grafik Fungsi Kuadrat', fontsize=14, fontweight='bold')
ax.grid(True, linestyle=':', alpha=0.6)
ax.legend(fontsize=11)

# Menampilkan grafik di Streamlit
st.pyplot(fig)

# Penjelasan Analisis Kurva
st.markdown("---")
st.subheader("💡 Analisis Perubahan Kurva:")
col1, col2, col3 = st.columns(3)

with col1:
    st.markdown("**Pengaruh $a$:**")
    if a > 0:
        st.write("• Parabola terbuka ke **atas** (minimum).")
    else:
        st.write("• Parabola terbuka ke **bawah** (maksimum).")
    st.write(f"• Nilai $|a| = {abs(a):.2f}$ menentukan tingkat kecuraman.")

with col2:
    st.markdown("**Pengaruh $b$:**")
    st.write(f"• Sumbu simetri berada di $x = {vertex_x:.2f}$.")
    if (a > 0 and b < 0) or (a < 0 and b > 0):
        st.write("• Puncak bergeser ke **kanan** sumbu Y.")
    else:
        st.write("• Puncak bergeser ke **kiri** sumbu Y.")

with col3:
    st.markdown("**Pengaruh $c$:**")
    st.write(f"• Memotong sumbu Y di titik $(0, {c:.1f})$.")
    st.write("• Menggeser kurva secara **vertikal** ke atas/bawah.")
