<h3 align="center">Zoom Clon</h3>

## <a name="table">Tabla de contenido</a>

1. [Introducción](#introducción)
2. [Pila tecnológica](#pila-tecnológica)
3. [Funciones](#funciones)
4. [Inicio rápido](#inicio-rápido)
5. [Fragmentos](#fragmentos)

## Tutorial

## <a name="introducción"> Introducción</a>

Construido con Next.js y TypeScript, este proyecto replica Zoom, una herramienta de videoconferencia ampliamente utilizada. Permite a los usuarios iniciar sesión, crear reuniones y acceder de forma segura a diversas funcionalidades de la reunión, como la grabación, el uso compartido de la pantalla y la gestión de participantes.

## <a name="pila-tecnológica"> Pila tecnológica</a>

- Next.js
- TypeScript
- Clerk
- getstream
- shadcn
- Tailwind CSS

## <a name="funciones"> Funciones</a>

**Autenticación**: Implementa funciones de autenticación y autorización mediante Clerk, lo que permite a los usuarios iniciar sesión de forma segura a través de inicio de sesión social o métodos tradicionales de correo electrónico y contraseña, al tiempo que garantiza los niveles de acceso y permisos adecuados dentro de la plataforma.

**Nueva reunión**: Inicie rápidamente una nueva reunión, configurando los ajustes de la cámara y el micrófono antes de unirse..

**Controles de la reunión**: los participantes tienen control total sobre los aspectos de la reunión, incluida la grabación, las reacciones emoji, el uso compartido de la pantalla, el silenciamiento/reactivación, los ajustes de sonido, el diseño de la cuadrícula, la vista de la lista de participantes y la administración individual de los participantes (fijar, silenciar, reactivar, bloquear, permitir compartir video).

**Salir de la reunión**: los participantes pueden abandonar una reunión o los creadores pueden finalizarla para todos los asistentes.

**Programar reuniones futuras**: Ingrese los detalles de la reunión (fecha, hora) para programar reuniones futuras, accesible en la página 'Próximas reuniones' para compartir el enlace o el inicio inmediato.

**Lista de reuniones anteriores**: acceda a una lista de reuniones celebradas anteriormente, incluidos los detalles y los metadatos.

**Ver reuniones grabadas**: Acceda a las grabaciones de reuniones anteriores para su revisión o referencia

**Sala personal**: Los usuarios tienen una sala personal con un enlace de reunión único para reuniones instantáneas, que se puede compartir con otros.

**Unirse a reuniones a través de un enlace**: Únase fácilmente a reuniones creadas por otros usuarios proporcionando un enlace.

**Funcionalidad segura en tiempo real**: Todas las interacciones dentro de la plataforma son seguras y ocurren en tiempo real, manteniendo la privacidad del usuario y la integridad de los datos.

**Diseño responsivo**: Sigue los principios del diseño responsivo para garantizar una experiencia de usuario óptima en todos los dispositivos, adaptándose sin problemas a diferentes tamaños y resoluciones de pantalla.

y muchos más, incluyendo la arquitectura del código y la reutilización.

## <a name="inicio-rápido"> Inicio rápido</a>

Siga estos pasos para configurar el proyecto localmente en su máquina.

**Prerrequisitos**

Asegúrese de tener instalado lo siguiente en su máquina:

- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en)
- [npm](https://www.npmjs.com/) (Node Package Manager)

**Clonación del repositorio**

```bash
git clone https://github.com/CRISHFAS/Zoom-clon
cd Zoom-clon
```

**Instalación**

Instale las dependencias del proyecto usando npm:

```bash
npm install
```

**Configurar variables de entorno**

Cree un nuevo archivo con un nombre `.env` en la raíz de su proyecto y agregue el siguiente contenido:

```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up

NEXT_PUBLIC_STREAM_API_KEY=
STREAM_SECRET_KEY=
```

Reemplace los valores de marcador de posición con sus credenciales reales de Clerk & getstream. Puede obtener estas credenciales registrándose en e [sitio web de Clerck](https://clerk.com/) y [sitio web de getstream](https://getstream.io/)

**Ejecución del proyecto**

```bash
npm run dev
```

Abra [http://localhost:3000](http://localhost:3000) en su navegador para ver el proyecto.

## <a name="fragmentos"> Fragmentos</a>

<details>
<summary><code>app/globals.css</code></summary>

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* ======== stream css overrides ======== */
.str-video__call-stats {
  max-width: 500px;
  position: relative;
}

.str-video__speaker-layout__wrapper {
  max-height: 700px;
}

.str-video__participant-details {
  color: white;
}

.str-video__menu-container {
  color: white;
}

.str-video__notification {
  color: white;
}

.str-video__participant-list {
  background-color: #1c1f2e;
  padding: 10px;
  border-radius: 10px;
  color: white;
  height: 100%;
}

.str-video__call-controls__button {
  height: 40px;
}

.glassmorphism {
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
}
.glassmorphism2 {
  background: rgba(18, 17, 17, 0.25);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

/* ==== clerk class override ===== */

.cl-userButtonPopoverActionButtonIcon {
  color: white;
}

.cl-logoBox {
  height: 40px;
}
.cl-dividerLine {
  background: #252a41;
  height: 2px;
}

.cl-socialButtonsIconButton {
  border: 3px solid #565761;
}

.cl-internal-wkkub3 {
  color: white;
}
.cl-userButtonPopoverActionButton {
  color: white;
}

/* =============================== */

@layer utilities {
  .flex-center {
    @apply flex justify-center items-center;
  }

  .flex-between {
    @apply flex justify-between items-center;
  }
}

/* animation */

.show-block {
  width: 100%;
  max-width: 350px;
  display: block;
  animation: show 0.7s forwards linear;
}

@keyframes show {
  0% {
    animation-timing-function: ease-in;
    width: 0%;
  }

  100% {
    animation-timing-function: ease-in;
    width: 100%;
  }
}
```

</details>

<details>
<summary><code>tailwind.config.ts</code></summary>

```typescript
import type { Config } from 'tailwindcss';

const config = {
  darkMode: ['class'],
  content: [
    './pages/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './app/**/*.{ts,tsx}',
    './src/**/*.{ts,tsx}',
  ],
  prefix: '',
  theme: {
    container: {
      center: true,
      padding: '2rem',
      screens: {
        '2xl': '1400px',
      },
    },
    extend: {
      colors: {
        dark: {
          1: '#1C1F2E',
          2: '#161925',
          3: '#252A41',
          4: '#1E2757',
        },
        blue: {
          1: '#0E78F9',
        },
        sky: {
          1: '#C9DDFF',
          2: '#ECF0FF',
          3: '#F5FCFF',
        },
        orange: {
          1: '#FF742E',
        },
        purple: {
          1: '#830EF9',
        },
        yellow: {
          1: '#F9A90E',
        },
      },
      keyframes: {
        'accordion-down': {
          from: { height: '0' },
          to: { height: 'var(--radix-accordion-content-height)' },
        },
        'accordion-up': {
          from: { height: 'var(--radix-accordion-content-height)' },
          to: { height: '0' },
        },
      },
      animation: {
        'accordion-down': 'accordion-down 0.2s ease-out',
        'accordion-up': 'accordion-up 0.2s ease-out',
      },
      backgroundImage: {
        hero: "url('/images/hero-background.png')",
      },
    },
  },
  plugins: [require('tailwindcss-animate')],
} satisfies Config;

export default config;
```

</details>

<details>
<summary><code>components/MeetingCard.tsx</code></summary>

```typescript
"use client";

import Image from "next/image";

import { cn } from "@/lib/utils";
import { Button } from "./ui/button";
import { avatarImages } from "@/constants";
import { useToast } from "./ui/use-toast";

interface MeetingCardProps {
  title: string;
  date: string;
  icon: string;
  isPreviousMeeting?: boolean;
  buttonIcon1?: string;
  buttonText?: string;
  handleClick: () => void;
  link: string;
}

const MeetingCard = ({
  icon,
  title,
  date,
  isPreviousMeeting,
  buttonIcon1,
  handleClick,
  link,
  buttonText,
}: MeetingCardProps) => {
  const { toast } = useToast();

  return (
    <section className="flex min-h-[258px] w-full flex-col justify-between rounded-[14px] bg-dark-1 px-5 py-8 xl:max-w-[568px]">
      <article className="flex flex-col gap-5">
        <Image src={icon} alt="upcoming" width={28} height={28} />
        <div className="flex justify-between">
          <div className="flex flex-col gap-2">
            <h1 className="text-2xl font-bold">{title}</h1>
            <p className="text-base font-normal">{date}</p>
          </div>
        </div>
      </article>
      <article className={cn("flex justify-center relative", {})}>
        <div className="relative flex w-full max-sm:hidden">
          {avatarImages.map((img, index) => (
            <Image
              key={index}
              src={img}
              alt="attendees"
              width={40}
              height={40}
              className={cn("rounded-full", { absolute: index > 0 })}
              style={{ top: 0, left: index * 28 }}
            />
          ))}
          <div className="flex-center absolute left-[136px] size-10 rounded-full border-[5px] border-dark-3 bg-dark-4">
            +5
          </div>
        </div>
        {!isPreviousMeeting && (
          <div className="flex gap-2">
            <Button onClick={handleClick} className="rounded bg-blue-1 px-6">
              {buttonIcon1 && (
                <Image src={buttonIcon1} alt="feature" width={20} height={20} />
              )}
              &nbsp; {buttonText}
            </Button>
            <Button
              onClick={() => {
                navigator.clipboard.writeText(link);
                toast({
                  title: "Link Copied",
                });
              }}
              className="bg-dark-4 px-6"
            >
              <Image
                src="/icons/copy.svg"
                alt="feature"
                width={20}
                height={20}
              />
              &nbsp; Copy Link
            </Button>
          </div>
        )}
      </article>
    </section>
  );
};

export default MeetingCard;
```

</details>
