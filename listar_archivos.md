```bash
# nano ~/.bashrc
# ~/.bashrc
# source ~/.bashrc

# Función para listar archivos con una extensión específica
listar_archivos() {
    local extensions=()
    local move_flag=false
    local target_dir="./archivos_encontrados"

    for arg in "$@"; do
        if [[ "$arg" == "--move" ]]; then
            move_flag=true
        else
            extensions+=("$arg")
        fi
    done

    if [[ ${#extensions[@]} -eq 0 ]]; then
        echo "Por favor, proporciona una extensión de archivo (por ejemplo, .mp4)"
        return 1
    fi

    # Crear directorio de destino si el flag esta activado
    if [[ "$move_flag" == "--move" ]]; then
        mkdir -p "$target_dir"
    fi

    for extension in "${extensions[@]}"; do
        find . -type f -name "*${extension}" 2>/dev/null | while IFS= read -r file; do
            echo "Found file: $file"
            if [[ "$move_flag" == "--move" ]]; then
                mv "$file" "$target_dir"
                echo "Moved $file to $target_dir"
            fi
        done
    done
}
```