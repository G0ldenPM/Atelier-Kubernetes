# Rendu — Atelier Kubernetes

> Complétez ce fichier au fil de l'atelier, puis faites un commit et un push (voir la section « Rendu » du README).

**Nom / Prénom :**
**Groupe :**

---

## Exercice 1 — Cluster

1. Combien de nœuds affiche `kubectl get nodes` ? Quel est le rôle de chacun ?
   >3 noeuds affichés : un serveur (control plane) et deux agents (workers)
2. Que montre `docker ps` ? Qu'est-ce qu'un « nœud » dans k3d, concrètement ?
   >docker ps montre la liste des noeuds. Un  noeud est un docker qui simule une machine.

## Exercice 2 — Premier déploiement

3. Quels objets Kubernetes ont été créés par `kubectl create deployment` ? (indice : `kubectl get all`)
   >un deployment, un replicaset et un pod
4. Vous avez supprimé le pod `web-...` : que s'est-il passé, et pourquoi ?
   >un nouveau pod avec un nom différent à été directement créé

## Exercice 3 — Modifier un conteneur en direct

5. Après suppression du pod, votre message « Bienvenue... » a-t-il survécu ? Pourquoi ?
   >Non, le message n'existe plus car la modification n'existait  que dans le pod supprimé et pas le nouveau.
6. Pourquoi le `port-forward` a-t-il cessé de fonctionner après la suppression du pod ?
   >parceque le tunnel pointe vers le pod supprimé

## Exercice 4 — Déclaratif

7. Quelle différence entre `kubectl create` et `kubectl apply` ?
   >kubectl create donne un ordre, « crée cet objet »   kubectl apply -f décrit l’état désiré dans un fichier YAML
8. À quoi sert le `selector` d'un Service ? Que se passe-t-il s'il ne correspond à aucun pod ?
   >selector définit quels pods reçoivent le trafic. Si il ne correspond à aucun pod le trafic n'arrive nulle part

## Exercice 5 — Scaling & mises à jour

9. Sur quels nœuds se trouvent vos 3 réplicas ? Collez la sortie de `kubectl get pods -l app=site -o wide`.
   >les 3 replicas sont repartis sur les 3 noeuds (2 agents et 1 server)
   ```
   $ kubectl get pods -o wide -w
   NAME                    READY   STATUS    RESTARTS   AGE   IP          NODE              NOMINATED NODE   READINESS GATES
   site-564c9bc484-f9z5s   1/1     Running   0          10m   10.42.1.6   k3d-lab-agent-0   <none>           <none>
   web-68d995574f-brczg    1/1     Running   0          40m   10.42.2.7   k3d-lab-agent-1   <none>           <none>
   site-564c9bc484-zczjm   0/1     Pending   0          0s    <none>      <none>            <none>           <none>
   site-564c9bc484-zczjm   0/1     Pending   0          0s    <none>      k3d-lab-agent-1   <none>           <none>
   site-564c9bc484-c567j   0/1     Pending   0          0s    <none>      <none>            <none>           <none>
   site-564c9bc484-c567j   0/1     Pending   0          0s    <none>      k3d-lab-server-0   <none>           <none>
   site-564c9bc484-zczjm   0/1     ContainerCreating   0          0s    <none>      k3d-lab-agent-1    <none>           <none>
   site-564c9bc484-c567j   0/1     ContainerCreating   0          0s    <none>      k3d-lab-server-0   <none>           <none>
   site-564c9bc484-zczjm   1/1     Running             0          1s    10.42.2.9   k3d-lab-agent-1    <none>           <none>
   site-564c9bc484-c567j   1/1     Running             0          8s    10.42.0.5   k3d-lab-server-0   <none>           <none>
   ```

10. Avec l'image `nginx:9.99`, quel statut avait le pod ? Quelle commande vous a donné la cause ?
    >le pod a le statut "ImagePullBackOff",  on utilise la commande "kubectl get pods -l app=site"
11. Pendant la panne, le site restait-il accessible ? Pourquoi ?
    >Le siterestait accessible car les 3 pods tournaient toujours.

## Exercice 6 — Portainer & Mario

12. URL publique de votre Mario :
    >https://obscure-space-goggles-g4v4476rwxwwhwqxq-8585.app.github.dev/
13. Retrouvez le Deployment `mario` en ligne de commande. Portainer et `kubectl` parlent-ils au même composant ? Lequel ?
    >Portainer et `kubectl` parlent au l'api serveur.

## Bonus (facultatif)

14. Bonus réalisés et remarques :
    >

---

**Score obtenu avec `./scripts/check.sh` :** ... / ...
