<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { createNoise2D } from 'simplex-noise'
import { Heart, MessageCircle, Repeat2, Share, MoreHorizontal, Verified } from 'lucide-vue-next'

gsap.registerPlugin(ScrollTrigger)

// ✅ Strongly typed ref
const content = ref<HTMLDivElement | null>(null)

const services = [
    {
        id: 1,
        username: "MentorDanmark",
        handle: "@mentordanmark",
        verified: true,
        avatar: "/images/mentor.png",
        time: "2h",
        content: "Vi styrker unges faglige og personlige udvikling gennem mentoring 🌱 Vores mentorer giver støtte, motivation og selvtillid til at lykkes i skolen og livet.",
        hashtags: "#Mentoring #Læring #Selvtillid",
        likes: 312,
        retweets: 104,
        comments: 45,
        service: "Mentorordning for børn og unge",
        position: { left: '10%', rotation: -3 }
    },
    {
        id: 2,
        username: "Sundhedsstyrelsen",
        handle: "@sundhedsstyrelsen",
        verified: true,
        avatar: "/images/sundhed.png",
        time: "4h",
        content: "Næsten 600.000 danskere lever med en psykisk lidelse 🧠 Og op til 50% vil opleve én i deres levetid. Mental trivsel er en samfundsopgave. #mentaltrivsel",
        hashtags: "#PsykiskSundhed #Statistik #Forebyggelse",
        likes: 841,
        retweets: 204,
        comments: 72,
        service: "Mental sundhed i Danmark",
        position: { left: '11%', rotation: 1 }
    },
    {
        id: 3,
        username: "EnAfOsDK",
        handle: "@enafosdk",
        verified: true,
        avatar: "/images/enafos.png",
        time: "6h",
        content: "Ingen skal stå alene med psykiske udfordringer. Vi bekæmper stigma og fremmer åbenhed omkring mentale lidelser 💬 #DuErIkkeAlene",
        hashtags: "#PsykiskSygdom #Stigma #EnAfOs",
        likes: 678,
        retweets: 152,
        comments: 65,
        service: "Antistigmatiseringskampagne",
        position: { left: '12%', rotation: 2 }
    },
    {
        id: 4,
        username: "PsykologPriser",
        handle: "@terapidanmark",
        verified: true,
        avatar: "/images/terapi.png",
        time: "8h",
        content: "Pris for privat psykolog: ca. 1.250 kr/session 🧾 Med henvisning fra egen læge kan du få gratis hjælp – men ventetid kan være op til 52 uger.",
        hashtags: "#Terapi #Psykolog #Ventetid",
        likes: 485,
        retweets: 133,
        comments: 58,
        service: "Statistik over terapipriser og adgang",
        position: { left: '13%', rotation: -1 }
    },
    {
        id: 5,
        username: "ABCMentalHealth",
        handle: "@abc_sundhed",
        verified: true,
        avatar: "/images/abc.png",
        time: "12h",
        content: "Gør noget aktivt, socialt og meningsfuldt 💛 Det er nøglen til god mental sundhed ifølge ABC-projektet fra Københavns Universitet.",
        hashtags: "#MentalSundhed #ABC #Fællesskab",
        likes: 378,
        retweets: 101,
        comments: 49,
        service: "Trivselsfremmende initiativer",
        position: { left: '14%', rotation: 2 }
    }
];

services.push(
    {
        id: 6,
        username: "MentalityDK",
        handle: "@mentalitydk",
        verified: true,
        avatar: "/images/mentality.png",
        time: "1d",
        content: "Coaching og mentaltræning til unge og voksne 💬 Vi kombinerer mentoring med psykologisk indsigt for at styrke trivsel og selvværd.",
        hashtags: "#Mentoring #MentalTræning #Coaching",
        likes: 512,
        retweets: 143,
        comments: 39,
        service: "Mentoring og coaching",
        position: { left: '15%', rotation: -2 }
    },
    {
        id: 7,
        username: "StatistikDanmark",
        handle: "@dst_statistik",
        verified: true,
        avatar: "/images/statistik.png",
        time: "2d",
        content: "Ifølge Den Nationale Sundhedsprofil 2023 har 15 % af unge lav mental trivsel 😔 Stress og angst er stigende blandt 16-24-årige.",
        hashtags: "#Statistik #MentalSundhed #Unge",
        likes: 603,
        retweets: 178,
        comments: 66,
        service: "Statistik om mental trivsel",
        position: { left: '10.5%', rotation: 1 }
    },
    {
        id: 8,
        username: "PsykiatriPlus",
        handle: "@psykiatriplus",
        verified: true,
        avatar: "/images/psykiatri.png",
        time: "3d",
        content: "Vi tilbyder specialiseret psykiatrisk støtte i Ballerup 🏥 Fokus på akut hjælp, rehabilitering og trygge forløb for alle aldersgrupper.",
        hashtags: "#Psykiatri #Behandling #MentalSundhed",
        likes: 429,
        retweets: 97,
        comments: 52,
        service: "Psykiatrisk behandling",
        position: { left: '11.5%', rotation: -1 }
    },
    {
        id: 9,
        username: "Lyngemetoden",
        handle: "@lyngemetoden",
        verified: true,
        avatar: "/images/lyngemetoden.png",
        time: "4d",
        content: "Metode med dokumenteret effekt 🌿 4.9 stjerner på Trustpilot! Vi hjælper med angst, stress og lavt selvværd gennem samtaleterapi.",
        hashtags: "#Terapi #Stress #Selvværd",
        likes: 712,
        retweets: 203,
        comments: 88,
        service: "Privat terapi og mentaltræning",
        position: { left: '12.5%', rotation: 2 }
    },
    {
        id: 10,
        username: "BPoC_DK",
        handle: "@bpocdk",
        verified: true,
        avatar: "/images/bpoc.png",
        time: "5d",
        content: "Mentorprogram for studerende med minoritetsbaggrund 🎓 6-ugers forløb med fokus på karriere, trivsel og netværk i Danmark.",
        hashtags: "#Mentoring #Diversitet #Studieliv",
        likes: 388,
        retweets: 122,
        comments: 47,
        service: "Mentorprogram for BPoC-studerende",
        position: { left: '13.5%', rotation: -2 }
    }
);

onMounted(() => {
    content.value = document.querySelector('#content')
    if (!content.value) return // ✅ Type guard
    console.log('ScrollTrigger initialized')

    const noise2D = createNoise2D()

    for (let i = 0; i < 5000; i++) {
        const div = document.createElement('div')
        div.classList.add('circle')

        const n1 = noise2D(i * 0.003, i * 0.0033)
        const n2 = noise2D(i * 0.002, i * 0.001)

        Object.assign(div.style, {
            transform: `translate(${n2 * 200}px) rotate(${n2 * 270}deg) scale(${3 + n1 * 2}, ${3 + n2 * 2})`,
            boxShadow: `0 0 0 .2px hsla(${Math.floor(i * 0.3)}, 70%, 70%, .6)`,
            zIndex: -1,
        })

        content.value.appendChild(div)
    }

    const circles = document.querySelectorAll('.circle')
    const timeline = gsap.timeline({
        scrollTrigger: {
            trigger: "#content",
            scrub: 0.7,
            start: 'top 50%',
            end: 'bottom bottom'
        }
    })
    circles.forEach(circle => {
        timeline.to(circle, {
            opacity: 1
        })
    })

    // Animate service cards with staggered, organic timing
    const cards = document.querySelectorAll('.service-card')
    cards.forEach((card) => {
        // Add some randomness to the animation timing
        const delay = Math.random() * 0.5
        const yOffset = 50 + Math.random() * 100

        gsap.fromTo(card,
            {
                opacity: 0,
                y: yOffset,
                scale: 0.7,
                rotation: Math.random() * 10 - 5
            },
            {
                opacity: 1,
                y: 0,
                scale: 1,
                rotation: 0,
                duration: 1.2 + Math.random() * 0.8,
                delay: delay,
                ease: "power2.out",
                scrollTrigger: {
                    trigger: card,
                    start: "top 95%",
                    end: "bottom 5%",
                    toggleActions: "play none none reverse"
                }
            }
        )

        // Add subtle floating animation
        gsap.to(card, {
            y: "random(-1, 1)",
            rotation: "random(-1, 1)",
            duration: "random(3, 6)",
            repeat: -1,
            yoyo: true,
            ease: "sine.inOut",
            delay: Math.random() * 2
        })
    })
})
</script>

<template>
    <!--
    Author: Fabio Ottaviani
    Link: https://linktr.ee/supahfunk
    -->

    <div id="wrapper">
        <div id="content">

            <!-- Service cards container - collage style -->
            <div class="cards-collage">
                <div v-for="(service, index) in services" :key="service.id" class="service-card" :style="{
                    left: service.position.left,
                    transform: `rotate(${service.position.rotation}deg)`,
                    top: `${60 + (index * 35)}vh`,
                    zIndex: 10 + index
                }">
                    <!-- Card header -->
                    <div class="card-header">
                        <div class="user-info">
                            <img :src="service.avatar" :alt="service.username" class="avatar" />
                            <div class="user-details">
                                <div class="username-row">
                                    <span class="username">{{ service.username }}</span>
                                    <Verified v-if="service.verified" class="verified-icon" />
                                </div>
                                <span class="handle">{{ service.handle }}</span>
                            </div>
                        </div>
                        <div class="card-actions">
                            <span class="time">{{ service.time }}</span>
                            <MoreHorizontal class="more-icon" />
                        </div>
                    </div>

                    <!-- Card content -->
                    <div class="card-content">
                        <p class="tweet-text">{{ service.content }}</p>
                        <p class="hashtags">{{ service.hashtags }}</p>
                        <div class="service-tag">{{ service.service }}</div>
                    </div>

                    <!-- Card footer -->
                    <div class="card-footer">
                        <div class="action-item">
                            <MessageCircle class="action-icon" />
                            <span>{{ service.comments }}</span>
                        </div>
                        <div class="action-item">
                            <Repeat2 class="action-icon" />
                            <span>{{ service.retweets }}</span>
                        </div>
                        <div class="action-item">
                            <Heart class="action-icon" />
                            <span>{{ service.likes }}</span>
                        </div>
                        <div class="action-item">
                            <Share class="action-icon" />
                        </div>
                    </div>
                </div>
            </div>
            <button class="my-button" @click="'https://7kopper.dk/mentor'">Kickstart din rejse</button>

        </div>

    </div>
</template>

<style>
#wrapper {
    width: 100%;
    height: 100%;
    position: relative;
}

#content {
    width: 100%;
    height: 100%;
    position: relative;
    overflow: hidden;

}



.circle {
    width: 20px;
    height: 20px;
    border-radius: 40%;
    opacity: 0;
    margin: -19px auto;
    transition: transform 1s cubic-bezier(0.14, 0.15, 0.13, 0.99);
}

.hero-title {
    font-size: 4rem;
    font-weight: 800;
    margin-bottom: 1rem;
    background: linear-gradient(45deg, #fff, #f0f0f0);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    text-shadow: 0 4px 20px rgba(255, 255, 255, 0.3);
}

.hero-subtitle {
    font-size: 1.5rem;
    font-weight: 300;
    opacity: 0.9;
    max-width: 600px;
}

.cards-collage {
    position: relative;
    width: 100%;
    height: auto;
}

.service-card {
    position: absolute;
    background: rgba(255, 255, 255, 0.95);
    border-radius: 16px;
    padding: 1.5rem;
    box-shadow: 0 15px 50px rgba(0, 0, 0, 0.15);
    border: 1px solid rgba(255, 255, 255, 0.3);
    backdrop-filter: blur(15px);
    transition: all 0.4s ease;
    width: 320px;
    max-width: 90vw;
    transform-origin: center center;
}

.service-card:hover {
    transform: translateY(-8px) scale(1.02) !important;
    box-shadow: 0 25px 70px rgba(0, 0, 0, 0.2);
    z-index: 20 !important;
}

.card-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 1rem;
}

.user-info {
    display: flex;
    gap: 0.75rem;
    align-items: center;
}

.avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    object-fit: cover;
}

.user-details {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
}

.username-row {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.username {
    font-weight: 700;
    color: #1a1a1a;
    font-size: 0.95rem;
}

.verified-icon {
    width: 16px;
    height: 16px;
    color: #1d9bf0;
    fill: currentColor;
}

.handle {
    color: #536471;
    font-size: 0.9rem;
}

.card-actions {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    color: #536471;
}

.time {
    font-size: 0.9rem;
}

.more-icon {
    width: 16px;
    height: 16px;
    cursor: pointer;
    opacity: 0.6;
    transition: opacity 0.2s;
}

.more-icon:hover {
    opacity: 1;
}

.card-content {
    margin-bottom: 1rem;
}

.tweet-text {
    color: #1a1a1a;
    line-height: 1.5;
    margin-bottom: 0.75rem;
    font-size: 0.95rem;
}

.hashtags {
    color: #1d9bf0;
    font-size: 0.9rem;
    margin-bottom: 1rem;
}

.service-tag {
    display: inline-block;
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.card-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 0.75rem;
    border-top: 1px solid #eff3f4;
}

.action-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: #536471;
    cursor: pointer;
    transition: color 0.2s;
    font-size: 0.9rem;
}

.action-item:hover {
    color: #1d9bf0;
}

.action-icon {
    width: 18px;
    height: 18px;
}

.my-button {
    background-color: var(--kopper-lilac);
    color: var(--kopper-dark-text);
    padding: 0.8rem 1.4rem;
    margin: 3rem 0;
    display: block;
    position: absolute;
    bottom: 0;
    left: 50%;
    border: none;
    border-radius: 12px;
    font-size: 1rem;
    font-family: inherit;
    font-weight: bold;
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
    width: fit-content;
    z-index: 1000;
}

.my-button:hover {
    background-color: color-mix(in srgb, var(--color-accent) 90%, #ffffff 10%);
    transform: translateY(-1px);
}

.my-button:focus {
    outline: 2px solid var(--color-secondary);
    outline-offset: 3px;
}



/* Mobile Responsive Styles */
@media (max-width: 768px) {
    #wrapper {
        overflow-x: hidden;
    }

    #content {
        overflow-x: hidden;
    }

    .service-card:hover {
        transform: translateY(-5px) scale(1.02) !important;
    }

    .my-button {
        margin: 2rem auto;
        padding: 0.7rem 1.2rem;
        font-size: 0.95rem;
    }
}

@media (max-width: 480px) {
    .service-card {
        width: 100%;
        max-width: 300px;
        padding: 0.875rem;
    }

    .card-header {
        margin-bottom: 0.75rem;
    }

    .username {
        font-size: 0.9rem;
    }

    .tweet-text {
        font-size: 0.9rem;
    }

    .hashtags {
        font-size: 0.85rem;
    }

    .service-tag {
        font-size: 0.75rem;
        padding: 0.4rem 0.8rem;
    }

    .action-item {
        font-size: 0.85rem;
    }

    .action-icon {
        width: 16px;
        height: 16px;
    }

    .my-button {
        padding: 0.6rem 1rem;
        font-size: 0.9rem;
        margin: 1.5rem auto;
    }
}
</style>