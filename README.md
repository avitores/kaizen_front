# Kaizen Front por Alfonso Vítores.

## Características

- **Nuxt**
- **Vue**
- **TypeScript**
- **SSR**
- **Axios**
- **pug**
- **Jest**
- **Lint**
- **prettier**

## Inicio

```
npx create-nuxt-app kaizen-front
```

```
npm run build
```

```
npm start
npx nuxt dev (modo development)
```

## Confirguración de Typescript

"nuxt-config.js"

Para que no haya conflicto de puertos con backend

```
  server: {
    port: 3001
  },
```

Para llamar al API de backend

```
axios: {
	baseURL: process.env.API_URL || 'http://localhost:3000',
},
```

## Source

```
/pages
  ├── /tasks
  │    ├── index.vue          # Listado de tareas
  │    ├── new.vue            # Página para crear una nueva tarea
  │    ├── edit.vue           # Página para editar una tarea
  │    └── _id.vue            # Página para visualizar una tarea por ID

/components
  ├── ...

...
```
