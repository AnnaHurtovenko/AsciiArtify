### Встановлення системи ArgoCD

1. Створення кластера k3d з назвою argo:
    ```bash
    k3d cluster create argo
    ```

2. Перевірка інформації про кластер Kubernetes:
    ```bash
    kubectl cluster-info
    ```

3. Створення неймспейсу для ArgoCD:
    ```bash
    kubectl create namespace argocd
    ```

4. Застосування маніфестів для встановлення ArgoCD:
    ```bash
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    ```

5. Перевірка ресурсів ArgoCD:
    ```bash
    kubectl get all -n argocd
    ```

6. Перевірка стану подів ArgoCD:
    ```bash
    kubectl get pod -n argocd -w
    ```

7. Перенаправлення портів для доступу до інтерфейсу ArgoCD через веб-браузер:
    ```bash
    kubectl port-forward svc/argocd-server -n argocd 8080:443&
    ```

8. Логін у веб-інтерфейс ArgoCD:
    - Логін: `admin`
    - Пароль можна отримати за допомогою команди:
        ```bash
        kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"
        ```
    - Декодувати та вивести пароль можна так:
        ```bash
        kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
        ```

