```bash
# ~/.bashrc

# Función para listar archivos con una extensión específica
listar_archivos() {
    local extension="$1"
    local move_flag="$2"
    local target_dir="./archivos_encontrados"

    if [[ -z "$extension" ]]; then
        echo "Por favor, proporciona una extensión de archivo (por ejemplo, .mp4)"
        return 1
    fi

    # Crear directorio de destino si el flag esta activado
    if [[ "$move_flag" == "--move" ]]; then
        mkdir -p "$target_dir"
    fi

    find . -type f -name "*${extension}" 2>/dev/null | while IFS= read -r file; do
        echo "Found file: $file"
        if [[ "$move_flag" == "--move" ]]; then
            mv "$file" "$target_dir"
            echo "Move $file to $target_dir"
        fi

    done
}
```