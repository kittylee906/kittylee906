

        self.fotos = []
        self.index = 0

        self.label = tk.Label(root, text="Seu álbum vai aparecer aqui", font=("Comic Sans MS", 14), bg="#ffe6f0")
        self.label.pack(pady=10)

        self.canvas = tk.Label(root, bg="#ffe6f0")
        self.canvas.pack()

        botao_frame = tk.Frame(root, bg="#ffe6f0")
        botao_frame.pack(pady=10)

        self.btn_anterior = tk.Button(botao_frame, text="⬅️ Anterior", command=self.mostrar_anterior, font=("Arial", 10))
        self.btn_anterior.grid(row=0, column=0, padx=10)

        self.btn_proximo = tk.Button(botao_frame, text="Próxima ➡️", command=self.mostrar_proxima, font=("Arial", 10))
        self.btn_proximo.grid(row=0, column=1, padx=10)

        self.btn_carregar = tk.Button(root, text="📂 Carregar Fotos", command=self.carregar_fotos, font=("Arial", 12), bg="#ffb6c1")
        self.btn_carregar.pack(pady=10)

    def carregar_fotos(self):
        caminhos = filedialog.askopenfilenames(title="Escolha suas fotos fofas", filetypes=[("Imagens", "*.png *.jpg *.jpeg")])
        if caminhos:
            self.fotos = list(caminhos)
            self.index = 0
            self.mostrar_imagem()

    def mostrar_imagem(self):
        if not self.fotos:
            return
        imagem = Image.open(self.fotos[self.index])
        imagem.thumbnail((500, 500))
        foto = ImageTk.PhotoImage(imagem)
        self.canvas.configure(image=foto)
        self.canvas.image = foto
        nome = os.path.basename(self.fotos[self.index])
        self.label.config(text=f"Foto {self.index + 1} de {len(self.fotos)}: {nome}")

    def mostrar_anterior(self):
        if self.index > 0:
            self.index -= 1
            self.mostrar_imagem()

    def mostrar_proxima(self):
        if self.index < len(self.fotos) - 1:
            self.index += 1
            self.mostrar_imagem()

if __name__ == "__main__":
    root = tk.Tk()
    app = AlbumFofo(root)
    root.mainloop()
