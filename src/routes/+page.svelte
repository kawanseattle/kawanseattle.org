<script lang="ts">
	import { onMount } from 'svelte';
	import { base } from '$app/paths';

	const programs = [
		{
			title: 'Explore Seattle',
			description: 'Discover the city with people who are excited to experience it alongside you.',
			activities: ['Monthly city trips', 'Local landmarks', 'Seasonal outings']
		},
		{
			title: 'Community & Events',
			description: 'Build genuine friendships through relaxed gatherings designed for connection.',
			activities: ['Game nights', 'Holiday celebrations', 'Monthly gatherings']
		},
		{
			title: 'Study Together',
			description: 'Find encouragement and practical support throughout your academic journey.',
			activities: ['Study buddy matching', 'Group study sessions', 'Tutoring support']
		},
		{
			title: 'Guidance & Mentorship',
			description: 'Get thoughtful guidance from someone who understands what starting over feels like.',
			activities: ['One to one mentorship', 'College planning', 'Campus resources']
		},
		{
			title: 'Career Development',
			description: 'Take confident next steps with practical tools and a supportive professional network.',
			activities: ['Resume reviews', 'Interview practice', 'Career networking']
		}
	];

	const stories = [
		{
			quote:
				'My mentor helped me turn a confusing process into a clear plan. I arrived feeling prepared and supported.',
			name: 'Nadia Rahman',
			detail: 'Bangladesh → Canada',
			image:
				'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'Kawan connected me with students who understood exactly what I was going through.',
			name: 'Mateo Silva',
			detail: 'Brazil → Germany',
			image:
				'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=240&q=85'
		},
		{
			quote:
				'I found a scholarship I would never have discovered on my own. It changed what felt possible.',
			name: 'Amara Okafor',
			detail: 'Nigeria → United Kingdom',
			image:
				'https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=240&q=85'
		}
	];

	let menuOpen = false;
	let storyIndex = 0;
	let email = '';
	let submitted = false;
	let heroElement: HTMLElement;

	function subscribe() {
		if (email.trim()) {
			submitted = true;
			email = '';
		}
	}

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				for (const entry of entries) {
					if (entry.isIntersecting) {
						entry.target.classList.add('visible');
						observer.unobserve(entry.target);
					}
				}
			},
			{ threshold: 0.12 }
		);

		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));

		const updateHeroFade = () => {
			if (!heroElement) return;
			const progress = Math.min(window.scrollY / Math.max(heroElement.offsetHeight, 1), 1);
			heroElement.style.setProperty('--hero-scroll-fade', String(1 - progress * 0.28));
		};
		window.addEventListener('scroll', updateHeroFade, { passive: true });
		updateHeroFade();

		return () => {
			observer.disconnect();
			window.removeEventListener('scroll', updateHeroFade);
		};
	});
</script>

<svelte:head>
	<title>Kawan | Your journey. Our guidance.</title>
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label="Kawan home">
		<img class="header-logo" src={`${base}/images/kawan-logo.png`} alt="Kawan Seattle" />
	</a>

	<nav class:open={menuOpen} aria-label="Primary navigation">
		<a href="#about" onclick={() => (menuOpen = false)}>About</a>
		<a href="#programs" onclick={() => (menuOpen = false)}>How we help</a>
		<a href="#stories" onclick={() => (menuOpen = false)}>Stories</a>
	</nav>

	<a class="desktop-cta" href="#connect">Connect</a>
	<button
		class="menu-button"
		class:active={menuOpen}
		aria-label="Toggle navigation"
		aria-expanded={menuOpen}
		onclick={() => (menuOpen = !menuOpen)}
	>
		<span></span><span></span>
	</button>
</header>

<main id="top">
	<section class="hero" bind:this={heroElement}>
		<div class="hero-minimal">
			<div class="hero-illustrations" aria-hidden="true">
				<img class="hero-illustration illustration-space-needle" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-board-game" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-water-taxi" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
				<img class="hero-illustration illustration-hiking" src={`${base}/images/kawan-hero-seattle-sketches.png`} alt="" />
			</div>
			<div class="hero-content">
				<p class="hero-kicker">Welcome to</p>
				<h1><span class="kawan-script">KAWAN</span></h1>
				<p class="hero-statement">A friend for your journey.</p>
				<p class="hero-tagline">Helping international students settle in, build meaningful friendships, and navigate life in Seattle.</p>
				<div class="hero-actions">
					<a class="button" href="#connect">Get Connected <span>↗</span></a>
				</div>
			</div>
		</div>
	</section>
	<section class="about section-wrap" id="about">
		<div class="illustration-band reveal" id="our-story">
			<div class="illustration-copy">
				<p class="about-eyebrow">about us</p>
				<h2>It starts with a friend.</h2>
				<p class="story-lead"><strong>KAWAN means “friend” in Indonesian.</strong></p>
				<p><strong>Founded by international students, we understand the challenges of moving to a new country—from navigating school and everyday life to building friendships and planning for the future.</strong></p>
				<p><strong>We're here to help students settle into life in the U.S., build lasting friendships, and find a community that walks alongside them.</strong></p>
			</div>
			<figure class="about-photo-frame">
				<div class="about-photo-crop"><img src={`${base}/images/kawan-community-christmas-2025.jpeg`} alt="KAWAN community members gathering at Evergreen Christmas Lights in 2025" /></div>
			</figure>
		</div>
		<div class="belief-section">
			<div class="belief-heading reveal">
				<p class="about-eyebrow">our direction</p>
				<h2>What drives us.</h2>
			</div>
			<div class="about-grid">
			<article class="about-card reveal" id="our-vision">
				<div class="belief-label"><p class="about-label">our vision</p></div>
				<div class="belief-copy">
					<h3>Building a generation<br />that thrives.</h3>
					<p class="about-description">Building a generation of international students who thrive in life relationally, academically, and professionally, and empower those who come after them.</p>
				</div>
			</article>
			<article class="about-card reveal" id="our-mission" style="--delay: 120ms">
				<div class="belief-label"><p class="about-label">our mission</p></div>
				<div class="belief-copy">
					<h3>Welcoming.<br />Connecting.<br />Supporting.</h3>
					<p class="about-description">Welcoming and connecting international students to the broader community while providing friendship, support, resources, and career opportunities.</p>
				</div>
			</article>
			</div>
		</div>
	</section>

	<section class="programs section-wrap" id="programs">
		<div class="journey-section-heading reveal">
			<p class="about-eyebrow">How Kawan Supports You</p>
			<h2>Practical support, shared with care.</h2>
			<p>From discovering Seattle to planning what comes next, you’ll find people and resources for every part of student life.</p>
		</div>
		<div class="program-grid minimal">
			{#each programs as program, index}
				<article class="program-card reveal" style={`--delay: ${index * 75}ms`}>
					<div class="card-icon">
						{#if index === 0}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true"><path d="M8 29c7-10 13-17 24-21M9 11c6 2 10 6 12 12m-11 6 8 2 2-8" /></svg>
						{:else if index === 1}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true"><path d="M20 32s-12-6.3-12-14.2A7 7 0 0 1 20 12.4a7 7 0 0 1 12 5.4C32 25.7 20 32 20 32Z" /></svg>
						{:else if index === 2}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true"><path d="M7 11c5-2 9-1 13 2v18c-4-3-8-4-13-2zm26 0c-5-2-9-1-13 2v18c4-3 8-4 13-2z" /></svg>
						{:else if index === 3}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true"><circle cx="15" cy="14" r="5"/><circle cx="27" cy="18" r="4"/><path d="M6 31c1-7 5-10 9-10s8 3 9 10m0-6c5-2 9 1 10 6" /></svg>
						{:else}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true"><path d="M7 30V13h26v17M14 13V9h12v4M5 30h30M14 20h12" /></svg>
						{/if}
					</div>
					<h3>{program.title}</h3>
					<p>{program.description}</p>
					<ul>{#each program.activities as activity}<li>{activity}</li>{/each}</ul>
					<a href="#connect" aria-label={`Explore ${program.title}`}>Learn more <span>↗</span></a>
				</article>
			{/each}
		</div>
	</section>

	<section class="community-photo-break reveal" aria-label="KAWAN community">
		<img src={`${base}/images/kawan-community-outing.jpeg`} alt="KAWAN students and families enjoying a community outing by the water" />
		<p>Community begins by showing up for one another.</p>
	</section>

	<section class="stories section-wrap" id="stories">
		<div class="journey-section-heading stories-heading reveal">
			<p class="about-eyebrow">belonging</p>
			<h2>The journey becomes a shared one.</h2>
		</div>
		<div class="story-card reveal">
			<div class="quote-mark">"</div>
			<blockquote>{stories[storyIndex].quote}</blockquote>
			<div class="student">
				<img src={stories[storyIndex].image} alt={stories[storyIndex].name} />
				<div><strong>{stories[storyIndex].name}</strong><span>{stories[storyIndex].detail}</span></div>
			</div>
			<div class="story-progress">
				{#each stories as _, index}
					<button class:active={index === storyIndex} onclick={() => (storyIndex = index)} aria-label={`Show story ${index + 1}`}></button>
				{/each}
			</div>
		</div>
	</section>

	<section class="cta-minimal" id="connect">
		<div class="section-wrap">
			<div class="cta-content reveal">
				<p class="about-eyebrow">Get connected</p>
				<h2>There’s a place for you here.</h2>
				<p>Ready to begin your journey? Meet people who understand and find a community that will walk alongside you.</p>
				<div class="cta-actions"><a class="button large" href="mailto:hello@kawan.org">Get Connected <span>↗</span></a><a class="text-link" href="mailto:volunteer@kawan.org">Volunteer with us</a></div>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="footer-main section-wrap">
		<div class="footer-brand">
			<a class="footer-identity" href="#top" aria-label="KAWAN Seattle home">
				<img src={`${base}/images/kawan-logo.png`} alt="" aria-hidden="true" />
				<span><strong>KAWAN</strong><small>SEATTLE</small></span>
			</a>
			<p>A friend for your journey.</p>
		</div>
		<div class="footer-links">
			<div><strong>LINKS</strong><a href="#programs">How we help</a><a href="#stories">Stories</a></div>
			<div><strong>GET INVOLVED</strong><a href="mailto:volunteer@kawan.org">Volunteer</a><a href="mailto:hello@kawan.org">Contact us</a></div>
		</div>
	</div>
	<div class="footer-bottom section-wrap">
		<span>© 2026 KAWAN Seattle.</span>
	</div>
</footer>

<style>
	:global(.reveal) {
		opacity: 0;
		transform: translateY(24px);
		transition: opacity 0.7s ease, transform 0.7s ease;
		transition-delay: var(--delay, 0ms);
	}

	:global(.reveal.visible) {
		opacity: 1;
		transform: translateY(0);
	}

	.site-header {
		position: absolute;
		z-index: 20;
		top: 18px;
		left: 50%;
		display: flex;
		width: min(1280px, calc(100% - 64px));
		height: 88px;
		align-items: center;
		justify-content: space-between;
		padding: 0 18px 0 20px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 999px;
		background: rgba(250, 248, 245, 0.7);
		backdrop-filter: blur(8px);
		box-shadow: 0 14px 40px rgba(91, 74, 66, 0.05);
		transform: translateX(-50%);
	}

	.brand {
		display: inline-flex;
		align-items: center;
		font-family: 'Quicksand', sans-serif;
		font-size: 20px;
		font-weight: 700;
		letter-spacing: -0.8px;
		text-transform: lowercase;
	}

	:global(.brand-mark) {
		display: inline-flex;
		width: 42px;
		height: 42px;
		margin-right: 9px;
		color: var(--forest);
	}

	nav {
		display: flex;
		gap: 50px;
		margin-left: 90px;
	}

	nav a {
		position: relative;
		color: var(--ink);
		font-size: 18px;
		font-weight: 500;
	}

	nav a::after {
		position: absolute;
		right: 0;
		bottom: -7px;
		left: 0;
		height: 2px;
		background: var(--gold);
		content: '';
		transform: scaleX(0);
		transition: transform 0.25s ease;
	}

	nav a:hover::after {
		transform: scaleX(1);
	}

	.button {
		display: inline-flex;
		min-height: 52px;
		align-items: center;
		justify-content: center;
		gap: 13px;
		padding: 0 23px;
		border: 1px solid rgba(61, 61, 61, 0.08);
		border-radius: 13px;
		color: #fff;
		background: #6d5c54;
		box-shadow: 0 8px 20px rgba(109, 92, 84, 0.16);
		font-size: 14px;
		font-weight: 600;
		transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
	}

	.button:hover {
		background: #584943;
		transform: translateY(-1px);
		box-shadow: 0 11px 24px rgba(88, 73, 67, 0.2);
	}

	:global(.button.small) {
		min-height: 42px;
		padding: 0 17px;
	}

	.button.large {
		min-height: 60px;
		padding: 0 32px;
		font-size: 16px;
	}

	:global(.button.gold) {
		color: var(--ink);
		background: var(--gold);
		box-shadow: none;
	}

	:global(.button.gold:hover) {
		background: #ffc979;
	}

	.menu-button {
		display: none;
		width: 44px;
		height: 44px;
		padding: 13px 10px;
		border-radius: 50%;
		background: var(--forest);
	}

	.menu-button span {
		display: block;
		width: 100%;
		height: 2px;
		margin: 5px 0;
		background: white;
		transition: transform 0.2s ease;
	}

	/* Hero Section */
	.hero {
		--hero-scroll-fade: 1;
		position: relative;
		min-height: 100vh;
		overflow: hidden;
		background: radial-gradient(circle at 20% 20%, rgba(232, 196, 119, 0.18), transparent 22%),
			radial-gradient(circle at 80% 10%, rgba(155, 143, 134, 0.13), transparent 24%),
			linear-gradient(135deg, #faf8f5 0%, #ede4db 100%);
	}

	.hero::before,
	.hero::after {
		position: absolute;
		content: '';
		border-radius: 50%;
		pointer-events: none;
	}

	.hero::before {
		right: -80px;
		bottom: -70px;
		width: 320px;
		height: 320px;
		background: rgba(232, 196, 119, 0.12);
	}

	.hero::after {
		left: -60px;
		top: 60px;
		width: 200px;
		height: 200px;
		background: rgba(155, 143, 134, 0.08);
	}

	.hero-minimal {
		display: flex;
		width: min(1280px, calc(100% - 64px));
		height: 100vh;
		min-height: 760px;
		margin: auto;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}

	.hero-content {
		position: relative;
		z-index: 2;
		text-align: center;
		max-width: 600px;
	}

	h1 {
		max-width: 100%;
		margin: 0 0 22px 0;
		color: var(--ink);
		font-family: 'Cormorant Garamond', serif;
		font-size: clamp(72px, 8vw, 128px);
		font-weight: 600;
		line-height: 1.1;
		letter-spacing: -2px;
		text-transform: lowercase;
	}

	.kawan-script {
		font-family: 'Cormorant Garamond', serif;
		font-size: 1.35em;
		font-weight: 800;
		letter-spacing: -1px;
		color: var(--forest);
	}

	:global(.welcome-to-text) {
		font-size: 0.45em;
		font-weight: 500;
	}

	.hero-tagline {
		max-width: 100%;
		margin: 0 0 40px 0;
		color: var(--muted);
		font-size: 22px;
		line-height: 1.6;
		text-transform: lowercase;
	}

	.hero-actions {
		display: flex;
		justify-content: center;
		gap: 20px;
		margin-top: 30px;
	}

	/* Hero Shape */
	:global(.hero-shape) {
		display: none;
	}

	/* About Section */
	.about {
		position: relative;
		min-height: 100vh;
		padding: 120px 0 110px;
		background: radial-gradient(circle at top left, rgba(232, 196, 119, 0.16), transparent 30%),
			linear-gradient(180deg, #f5eeea 0%, #f7f1eb 100%);
	}

	.about::before {
		position: absolute;
		inset: 80px auto auto 8%;
		width: 280px;
		height: 280px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 50%;
		content: '';
	}

	.about::after {
		position: absolute;
		right: 10%;
		bottom: 12%;
		width: 220px;
		height: 220px;
		border-radius: 50%;
		background: rgba(155, 143, 134, 0.08);
		content: '';
	}

	:global(.about-intro) {
		position: relative;
		z-index: 1;
		max-width: 720px;
		margin: 0 auto 52px;
		text-align: center;
	}

	.about-eyebrow {
		margin: 0;
		color: var(--muted);
		font-size: 12px;
		font-weight: 800;
		letter-spacing: 2px;
		text-transform: uppercase;
	}

	.about-grid {
		position: relative;
		z-index: 1;
		display: grid;
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 24px;
		max-width: 1180px;
		margin: 0 auto;
	}

	.about-card {
		display: flex;
		flex-direction: column;
		gap: 18px;
		min-height: 300px;
		padding: 34px 28px 30px;
		border: 1px solid rgba(107, 83, 72, 0.1);
		border-radius: 24px;
		background: rgba(255, 255, 255, 0.28);
		box-shadow: 0 18px 40px rgba(91, 74, 66, 0.03);
		transition: transform 0.25s ease, box-shadow 0.25s ease;
	}

	.about-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 24px 48px rgba(91, 74, 66, 0.06);
	}

	.about-label {
		margin: 0;
		font-size: 11px;
		font-weight: 800;
		letter-spacing: 1.8px;
		text-transform: uppercase;
		color: var(--muted);
	}

	.about-card h3 {
		margin: 0;
		font-size: clamp(24px, 2vw, 32px);
		line-height: 1.15;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -0.7px;
		text-transform: lowercase;
	}

	.about-description {
		margin: 0;
		font-size: 16px;
		line-height: 1.75;
		color: var(--muted);
	}

	@media (max-width: 900px) {
		.about {
			min-height: auto;
		}

		.about-grid {
			grid-template-columns: 1fr;
		}
	}

	/* Programs Section */
	.program-grid.minimal {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 24px;
		margin-top: 60px;
	}

	.program-card {
		padding: 48px 32px;
		border-radius: 18px;
		display: flex;
		flex-direction: column;
		gap: 24px;
		border: 1px solid rgba(107, 83, 72, 0.08);
		box-shadow: 0 18px 36px rgba(91, 74, 66, 0.04);
		transition: transform 0.25s ease, box-shadow 0.25s ease;
	}

	.program-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 22px 44px rgba(91, 74, 66, 0.06);
	}

	.card-icon {
		width: 60px;
		height: 60px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--ink);
	}

	.card-icon svg {
		width: 100%;
		height: 100%;
	}

	.program-card h3 {
		margin: 0;
		font-size: 28px;
		line-height: 1.2;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -0.6px;
	}

	.program-card a {
		color: var(--ink);
		font-size: 14px;
		font-weight: 700;
		text-decoration: none;
		display: inline-flex;
		align-items: center;
		gap: 8px;
		border-bottom: 1px solid var(--ink);
		padding-bottom: 5px;
		width: fit-content;
	}

	/* Mentor Section */
	:global(.mentor-section) {
		padding: 120px 0;
		background: #ede4db;
	}

	:global(.mentor-minimal) {
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}

	:global(.mentor-dot) {
		width: 80px;
		height: 80px;
		border: 2px solid var(--forest);
		border-radius: 50%;
		margin: 0 auto 40px;
	}

	:global(.mentor-minimal) h2 {
		font-size: 48px;
		margin: 0 0 16px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -1px;
	}

	:global(.mentor-minimal) p {
		color: var(--muted);
		font-size: 16px;
		margin: 0 0 32px 0;
		line-height: 1.6;
	}

	/* Stories Section */
	.stories {
		padding: 100px 0;
	}

	.story-card {
		max-width: 720px;
		margin: 0 auto;
		padding: 60px;
		background: linear-gradient(180deg, rgba(245,238,234,0.95), rgba(255,255,255,0.7));
		border: 1px solid rgba(107, 83, 72, 0.08);
		border-radius: 24px;
		box-shadow: 0 22px 50px rgba(91, 74, 66, 0.04);
	}

	.quote-mark {
		font-size: 80px;
		color: var(--gold);
		line-height: 0.6;
		margin-bottom: 20px;
	}

	blockquote {
		margin: 0 0 40px 0;
		font-size: 24px;
		line-height: 1.6;
		color: var(--ink);
		font-style: italic;
	}

	.student {
		display: flex;
		align-items: center;
		gap: 16px;
		margin-bottom: 32px;
	}

	.student img {
		width: 60px;
		height: 60px;
		border-radius: 50%;
	}

	.student strong {
		display: block;
		color: var(--ink);
	}

	.student span {
		display: block;
		font-size: 13px;
		color: var(--muted);
	}

	.story-progress {
		display: flex;
		gap: 8px;
		justify-content: center;
	}

	.story-progress button {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: rgba(91, 74, 66, 0.2);
		border: none;
		cursor: pointer;
		transition: background 0.3s ease;
	}

	.story-progress button.active {
		background: var(--ink);
	}

	/* CTA Section */
	.cta-minimal {
		padding: 120px 0;
		background: radial-gradient(circle at top left, rgba(232, 196, 119, 0.18), transparent 30%),
			linear-gradient(135deg, #f0dccb 0%, #e8dfd6 100%);
	}

	.cta-content {
		text-align: center;
	}

	.cta-content h2 {
		font-size: 64px;
		margin: 0 0 40px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -2px;
	}

	/* Footer */
	footer {
		background: var(--cream);
		color: var(--ink);
		padding: 60px 0 20px;
	}

	.footer-main {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 60px;
		margin-bottom: 60px;
	}

	.footer-brand p {
		margin: 12px 0;
		color: var(--muted);
		font-size: 14px;
		line-height: 1.6;
	}

	.footer-links {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 40px;
	}

	.footer-links strong {
		display: block;
		font-size: 11px;
		font-weight: 800;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		margin-bottom: 16px;
		color: var(--muted);
	}

	.footer-links a {
		display: block;
		margin-bottom: 12px;
		color: var(--ink);
		text-decoration: none;
		font-size: 14px;
		transition: opacity 0.2s ease;
	}

	.footer-links a:hover {
		opacity: 0.6;
	}

	.footer-bottom {
		padding-top: 20px;
		border-top: 1px solid rgba(91, 74, 66, 0.1);
		display: flex;
		justify-content: space-between;
		font-size: 12px;
		color: var(--muted);
	}

	/* Utilities */
	.section-wrap {
		width: min(1280px, calc(100% - 64px));
		margin: 0 auto;
	}

	/* Responsive */
	@media (max-width: 768px) {
		.hero-minimal {
			flex-direction: column;
			gap: 40px;
			min-height: auto;
			padding: 60px 0;
		}

		h1 {
			font-size: clamp(48px, 10vw, 72px);
		}

		:global(.hero-shape) {
			display: none;
		}

		:global(.about-content) {
			grid-template-columns: 1fr;
			gap: 60px;
		}

		:global(.about-content) h3 {
			font-size: 24px;
		}

		nav {
			display: none;
		}

		.menu-button {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
		}

		.program-grid.minimal {
			grid-template-columns: 1fr;
		}

		.story-card {
			padding: 40px;
		}

		:global(.mentor-section) {
			padding: 60px 0;
		}

		.cta-minimal {
			padding: 60px 0;
		}

		.cta-content h2 {
			font-size: 42px;
		}

		.footer-main {
			grid-template-columns: 1fr;
			gap: 40px;
		}

		.footer-links {
			grid-template-columns: 1fr;
		}
	}

	/* Friendly, contemporary type and details */
	:global(body) {
		font-family: 'Inter', sans-serif;
	}

	h1,
	h2,
	h3,
	.kawan-script,
	.program-card h3,
	.cta-content h2 {
		font-family: 'Manrope', sans-serif;
	}

	h1 {
		font-weight: 600;
		letter-spacing: -4px;
	}

	:global(.welcome-to-text) {
		font-weight: 600;
		letter-spacing: -1px;
	}

	.kawan-script {
		position: relative;
		display: inline-block;
		z-index: 0;
		padding: 0 18px 6px;
		color: var(--ink);
		font-weight: 800;
		letter-spacing: -5px;
	}

	.kawan-script::before {
		position: absolute;
		z-index: -1;
		right: 0;
		bottom: 8px;
		left: 0;
		height: 32%;
		border-radius: 18px 8px 16px 10px;
		background: #dce5d7;
		content: '';
		transform: rotate(-1deg);
	}

	.program-card {
		border-radius: 24px;
		background: #fff;
		box-shadow: 0 12px 32px rgba(91, 74, 66, 0.055);
	}

	.program-card:nth-child(2) {
		transform: translateY(16px);
	}

	.program-card:nth-child(2):hover {
		transform: translateY(10px);
	}

	.button {
		border-radius: 13px;
	}

	@media (max-width: 768px) {
		h1 {
			letter-spacing: -2.5px;
		}

		.program-card:nth-child(2),
		.program-card:nth-child(2):hover {
			transform: none;
		}
	}

	.illustration-band {
		position: relative;
		display: grid;
		min-height: 540px;
		grid-template-columns: 0.8fr 1.2fr;
		align-items: center;
		gap: 24px;
		overflow: hidden;
		margin: 45px 0 80px;
		padding: 48px 34px 18px 58px;
		border-radius: 36px;
		background: #f1e9e1;
	}

	.illustration-band::before {
		position: absolute;
		top: -90px;
		right: -65px;
		width: 320px;
		height: 320px;
		border: 1px solid rgba(201, 134, 107, 0.25);
		border-radius: 50%;
		content: '';
	}

	:global(.illustration-band img) {
		position: relative;
		z-index: 1;
		width: 100%;
		filter: drop-shadow(0 18px 22px rgba(109, 92, 84, 0.08));
	}

	:global(.about-photo-frame) {
		position: relative;
		z-index: 1;
		margin: 0;
		padding: 10px 10px 15px;
		background: #fff;
		box-shadow: 0 18px 42px rgba(109, 92, 84, 0.12);
		transform: rotate(1.5deg);
		transition: transform 0.3s ease, box-shadow 0.3s ease;
	}

	:global(.about-photo-frame):hover {
		box-shadow: 0 22px 50px rgba(109, 92, 84, 0.16);
		transform: rotate(0deg) translateY(-3px);
	}

	:global(.about-photo-crop) {
		position: relative;
		aspect-ratio: 1.52;
		overflow: hidden;
		background: #eee7df;
	}

	:global(.about-photo-crop) img {
		position: absolute;
		top: 50%;
		left: 50%;
		width: 145%;
		max-width: none;
		filter: none;
		transform: translate(-50%, -50%);
	}

	.illustration-copy {
		position: relative;
		z-index: 2;
	}

	.illustration-copy p {
		max-width: 410px;
		margin: 0;
		color: var(--muted);
		font-size: 17px;
		line-height: 1.7;
	}

	:global(.hand-note) {
		display: inline-flex;
		align-items: center;
		gap: 10px;
		padding: 0;
		border: 0;
		border-radius: 0;
		background: transparent;
		color: #6d5c54;
		font-size: 11px;
		font-weight: 700;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		transform: none;
	}

	:global(.hand-note)::before {
		width: 24px;
		height: 1px;
		background: #c9866b;
		content: '';
	}

	.about-grid {
		align-items: start;
	}

	.about-card:nth-child(2) {
		margin-top: 28px;
	}

	.about-card:nth-child(3) {
		margin-top: 56px;
	}

	@media (max-width: 768px) {
		.illustration-band { min-height: 0; grid-template-columns: 1fr; padding: 38px 24px 10px; border-radius: 26px; }
		:global(.about-photo-frame) { margin-top: 20px; }
		.about-card:nth-child(2),.about-card:nth-child(3) { margin-top: 0; }
	}

	/* Quiet editorial header */
	.site-header {
		top: 0;
		width: min(1280px, calc(100% - 64px));
		height: 82px;
		padding: 0;
		border: 0;
		border-bottom: 1px solid rgba(61, 61, 61, 0.1);
		border-radius: 0;
		background: transparent;
		backdrop-filter: none;
		box-shadow: none;
	}

	.brand {
		display: flex;
		align-items: baseline;
		gap: 9px;
		font-family: 'Manrope', sans-serif;
		font-size: 19px;
		font-weight: 800;
		letter-spacing: -0.5px;
	}

	:global(.brand small) {
		color: var(--muted);
		font-family: 'Inter', sans-serif;
		font-size: 8px;
		font-weight: 700;
		letter-spacing: 2px;
	}

	nav {
		gap: 31px;
		margin-left: 0;
	}

	nav a {
		color: #56514e;
		font-size: 13px;
		font-weight: 500;
	}

	nav a::after {
		bottom: -8px;
		height: 1px;
		background: #6d5c54;
	}

	.desktop-cta {
		display: inline-flex;
		align-items: center;
		gap: 8px;
		padding: 9px 0 8px;
		border-bottom: 1px solid #6d5c54;
		color: #4e443f;
		font-size: 13px;
		font-weight: 600;
		transition: color 0.2s ease, gap 0.2s ease;
	}

	.desktop-cta:hover {
		gap: 12px;
		color: #c9866b;
	}

	@media (max-width: 768px) {
		.site-header { width: calc(100% - 36px); height: 72px; }
		.desktop-cta { display: none; }
		.menu-button { width: 36px; height: 36px; padding: 7px 4px; border-radius: 0; background: transparent; }
		.menu-button span { width: 24px; margin: 5px auto; background: #3d3d3d; }
	}

	/* Soft, contemporary refinement */
	.hero {
		background: linear-gradient(180deg, #fbf8f4 0%, #f4eee8 100%);
	}

	.hero::before,
	.hero::after,
	:global(.hero-shape),
	.illustration-band::before {
		display: none;
	}

	.kawan-script {
		color: #6d5c54;
		font-weight: 700;
		letter-spacing: -3px;
	}

	.kawan-script::before {
		height: 24%;
		bottom: 10px;
		border-radius: 3px;
		background: #dfe6da;
		transform: none;
	}

	.about {
		background: #fbf8f4;
	}

	.about::before {
		display: none;
	}

	.illustration-band {
		min-height: 500px;
		margin-top: 34px;
		padding: 52px;
		border: 1px solid rgba(109, 92, 84, 0.08);
		border-radius: 24px;
		background: #f3ede6;
	}

	:global(.about-photo-frame),
	:global(.about-photo-frame):hover {
		padding: 8px 8px 14px;
		border-radius: 18px;
		box-shadow: 0 16px 38px rgba(109, 92, 84, 0.1);
		transform: none;
	}

	:global(.about-photo-crop) {
		border-radius: 12px;
	}

	.about-card:nth-child(2),
	.about-card:nth-child(3),
	.program-card:nth-child(2),
	.program-card:nth-child(2):hover {
		margin-top: 0;
		transform: none;
	}

	.program-card {
		border-color: rgba(109, 92, 84, 0.08);
		box-shadow: 0 10px 28px rgba(109, 92, 84, 0.045);
	}

	.cta-minimal {
		background: #e7ece3;
	}

	@media (max-width: 768px) {
		.illustration-band { padding: 36px 22px 22px; border-radius: 18px; }
	}

	/* Warm display type for the opening statement */
	.hero h1,
	.hero :global(.welcome-to-text),
	.hero .kawan-script {
		font-family: 'Fraunces', serif;
	}

	.hero h1 {
		font-weight: 600;
		letter-spacing: -3px;
	}

	.hero :global(.welcome-to-text) {
		font-weight: 500;
		letter-spacing: -0.5px;
	}

	.hero .kawan-script {
		font-weight: 700;
		letter-spacing: -4px;
	}

	/* About story hierarchy */
	:global(.about-intro) {
		max-width: 760px;
		margin-bottom: 40px;
		text-align: center;
	}

	:global(.about-intro) h2,
	.belief-heading h2 {
		margin: 8px 0 0;
		color: var(--ink);
		font-family: 'Fraunces', serif;
		font-size: clamp(44px, 5vw, 66px);
		font-weight: 600;
		line-height: 1;
		letter-spacing: -2px;
	}

	.illustration-band {
		grid-template-columns: 1fr 1fr;
		gap: 58px;
		padding: 54px;
	}

	.illustration-copy p {
		max-width: 520px;
		margin: 0 0 18px;
		font-size: 15px;
		line-height: 1.75;
	}

	.illustration-copy .story-lead {
		margin-top: 24px;
		color: #4f4945;
		font-size: 17px;
	}

	.story-lead strong {
		color: var(--ink);
		font-weight: 650;
	}

	.belief-heading {
		max-width: 680px;
		margin: 90px auto 42px;
		text-align: center;
	}

	.belief-heading .about-eyebrow {
		margin-bottom: 0;
	}

	.about-grid {
		grid-template-columns: repeat(2, minmax(0, 1fr));
		max-width: 940px;
		margin-right: auto;
		margin-left: auto;
	}

	.about-card {
		min-height: 330px;
		padding: 42px;
		border: 1px solid rgba(109, 92, 84, 0.08);
		border-radius: 20px;
		background: #fff;
		box-shadow: 0 10px 28px rgba(109, 92, 84, 0.045);
	}

	.about-card:first-child {
		background: #eef1eb;
	}

	.about-card h3 {
		font-family: 'Manrope', sans-serif;
		font-size: 30px;
		line-height: 1.15;
		letter-spacing: -1.2px;
	}

	@media (max-width: 768px) {
		:global(.about-intro) { margin-bottom: 30px; }
		.illustration-band { grid-template-columns: 1fr; gap: 30px; }
		.belief-heading { margin-top: 70px; }
		.about-grid { grid-template-columns: 1fr; }
		.about-card { min-height: 0; padding: 32px; }
	}

	.hero-content {
		z-index: 3;
	}

	/* Full-bleed page frame */
	:global(main),
	:global(footer) {
		width: 100%;
	}

	.section-wrap {
		width: 100%;
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
	}

	.site-header {
		left: 0;
		width: 100%;
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
		transform: none;
	}

	.hero,
	.hero-minimal {
		width: 100%;
		min-height: 100svh;
	}

	.hero-minimal {
		max-width: none;
		padding-right: max(32px, calc((100vw - 1280px) / 2));
		padding-left: max(32px, calc((100vw - 1280px) / 2));
	}

	@media (max-width: 768px) {
		.section-wrap,
		.hero-minimal,
		.site-header {
			width: 100%;
			padding-right: 20px;
			padding-left: 20px;
		}
	}

	/* Refined Seattle editorial drawing */
	:global(.seattle-art) {
		position: absolute;
		z-index: 1;
		bottom: -6px;
		left: 50%;
		width: 100vw;
		height: auto;
		max-width: none;
		opacity: 0.72;
		filter: saturate(0.72) contrast(0.94);
		transform: translateX(-50%);
		pointer-events: none;
	}

	@media (max-width: 768px) {
		:global(.seattle-art) {
			left: 50%;
			width: 165vw;
			max-width: none;
			opacity: 0.64;
		}
	}

	/* Separate vision and mission statements */
	.about.section-wrap {
		padding-right: 32px;
		padding-left: 32px;
	}

	:global(.about-intro),
	.belief-heading {
		width: 100%;
		max-width: none;
	}

	.illustration-band {
		width: 100%;
	}

	.about-grid {
		display: grid;
		width: 100%;
		grid-template-columns: 1fr;
		gap: 0;
		max-width: none;
	}

	.about-card,
	.about-card:first-child {
		display: grid;
		min-height: 0;
		grid-template-columns: 190px 1fr;
		gap: 50px;
		align-items: start;
		padding: 48px 0;
		border: 0;
		border-top: 1px solid rgba(109, 92, 84, 0.18);
		border-radius: 0;
		background: transparent;
		box-shadow: none;
	}

	.about-card:last-child {
		border-bottom: 1px solid rgba(109, 92, 84, 0.18);
	}

	.about-card:hover {
		box-shadow: none;
		transform: none;
	}

	.belief-label {
		display: flex;
		align-items: baseline;
		gap: 14px;
	}

	:global(.belief-label span) {
		color: #c9866b;
		font-family: 'Fraunces', serif;
		font-size: 21px;
	}

	.belief-label .about-label {
		margin: 0;
	}

	.belief-copy h3 {
		max-width: 650px;
		margin: 0 0 16px;
		font-family: 'Fraunces', serif;
		font-size: clamp(34px, 4vw, 48px);
		font-weight: 600;
		line-height: 1.08;
		letter-spacing: -1.5px;
	}

	.belief-copy .about-description {
		max-width: 620px;
		margin: 0;
		font-size: 16px;
		line-height: 1.7;
	}

	@media (max-width: 768px) {
		.about.section-wrap {
			padding-right: 20px;
			padding-left: 20px;
		}

		.about-card,
		.about-card:first-child {
			grid-template-columns: 1fr;
			gap: 24px;
			padding: 38px 0;
		}
	}

	/* One continuous journey */
	:global(main) {
		position: relative;
		isolation: isolate;
		overflow: hidden;
		background:
			radial-gradient(circle at 12% 28%, rgba(201, 134, 107, 0.07), transparent 22%),
			radial-gradient(circle at 88% 67%, rgba(167, 180, 158, 0.1), transparent 24%),
			linear-gradient(180deg, #fbf8f4 0%, #f7f1ea 48%, #f5f3ec 76%, #eef2ea 100%);
	}

	:global(.journey-thread) {
		position: absolute;
		z-index: -1;
		inset: 78vh 0 0;
		pointer-events: none;
	}

	:global(.journey-thread) svg {
		display: block;
		width: 100%;
		height: 100%;
		overflow: visible;
	}

	:global(.journey-thread) path {
		fill: none;
		vector-effect: non-scaling-stroke;
	}

	:global(.journey-wash) {
		stroke: rgba(167, 180, 158, 0.12);
		stroke-width: 34;
		stroke-linecap: round;
	}

	:global(.journey-line) {
		stroke: rgba(160, 127, 105, 0.26);
		stroke-width: 1.5;
		stroke-dasharray: 2 8;
		stroke-linecap: round;
	}

	.about,
	:global(.mentor-section),
	.cta-minimal {
		background: transparent;
	}

	.about,
	.programs,
	:global(.mentor-section),
	.stories,
	.cta-minimal {
		position: relative;
		z-index: 1;
	}

	:global(.journey-prologue) {
		max-width: 620px;
		margin: 22px auto 0;
		color: var(--muted);
		font-family: 'Fraunces', serif;
		font-size: 19px;
		line-height: 1.65;
	}

	:global(.journey-vignette) {
		position: relative;
		z-index: 1;
		margin: 0;
		pointer-events: none;
	}

	:global(.journey-vignette img) {
		width: 100%;
		height: auto;
		filter: saturate(0.72);
	}

	:global(.journey-vignette figcaption) {
		position: absolute;
		bottom: 10%;
		left: 50%;
		padding: 8px 14px;
		border: 1px solid rgba(109, 92, 84, 0.1);
		border-radius: 999px;
		color: #6d625c;
		background: rgba(251, 248, 244, 0.82);
		backdrop-filter: blur(8px);
		font-size: 11px;
		font-weight: 650;
		letter-spacing: 1.1px;
		text-transform: uppercase;
		transform: translateX(-50%);
		white-space: nowrap;
	}

	:global(.journey-vignette figcaption span) {
		margin-right: 8px;
		color: #c9866b;
		font-family: 'Fraunces', serif;
		font-size: 15px;
	}

	:global(.journey-vignette-arrival) {
		width: min(1120px, 88vw);
		margin: -34px auto -150px;
		opacity: 0.75;
	}

	.illustration-band {
		z-index: 2;
		border-color: rgba(109, 92, 84, 0.06);
		background: rgba(243, 237, 230, 0.76);
		backdrop-filter: blur(4px);
	}

	.programs {
		padding-top: 150px;
		padding-bottom: 120px;
	}

	.journey-section-heading {
		max-width: 740px;
		margin: 0 auto 36px;
		text-align: center;
	}

	.journey-section-heading h2 {
		margin: 10px 0 18px;
		color: var(--ink);
		font-family: 'Fraunces', serif;
		font-size: clamp(42px, 5vw, 66px);
		font-weight: 600;
		line-height: 1.06;
		letter-spacing: -2px;
	}

	.journey-section-heading > p:last-child {
		max-width: 580px;
		margin: 0 auto;
		color: var(--muted);
		font-size: 16px;
		line-height: 1.7;
	}

	:global(.journey-vignette-daily) {
		width: min(1040px, 84vw);
		margin: -42px auto -170px;
		opacity: 0.6;
	}

	.program-grid.minimal {
		position: relative;
		z-index: 2;
		margin-top: 90px;
	}

	.program-card {
		border-color: rgba(109, 92, 84, 0.09);
		background: rgba(255, 255, 255, 0.7);
		backdrop-filter: blur(9px);
	}

	:global(.mentor-section) {
		padding: 150px 0;
	}

	:global(.mentor-minimal) {
		padding: 70px 42px;
		border-top: 1px solid rgba(109, 92, 84, 0.14);
		border-bottom: 1px solid rgba(109, 92, 84, 0.14);
	}

	:global(.mentor-dot) {
		display: none;
	}

	:global(.journey-marker) {
		position: relative;
		width: 70px;
		height: 42px;
		margin: 0 auto 24px;
	}

	:global(.journey-marker)::before,
	:global(.journey-marker)::after,
	:global(.journey-marker) span {
		position: absolute;
		border-radius: 50% 50% 48% 52%;
		content: '';
	}

	:global(.journey-marker)::before {
		inset: 3px 8px 5px 5px;
		background: rgba(167, 180, 158, 0.2);
		transform: rotate(-8deg);
	}

	:global(.journey-marker)::after {
		inset: 9px 3px 2px 13px;
		border: 1px solid rgba(201, 134, 107, 0.5);
		transform: rotate(7deg);
	}

	.stories {
		padding-top: 110px;
		padding-bottom: 130px;
	}

	.stories-heading {
		margin-bottom: 54px;
	}

	.story-card {
		background: rgba(255, 255, 255, 0.55);
		backdrop-filter: blur(9px);
	}

	.cta-minimal {
		padding: 150px 0 170px;
	}

	.cta-content h2 {
		font-family: 'Fraunces', serif;
		font-size: clamp(52px, 7vw, 88px);
		font-weight: 600;
	}

	@media (max-width: 768px) {
		:global(.journey-thread) {
			top: 72vh;
			opacity: 0.65;
		}

		:global(.journey-wash) {
			stroke-width: 20;
		}

		:global(.journey-vignette-arrival),
		:global(.journey-vignette-daily) {
			width: 150vw;
			margin-left: -35vw;
		}

		:global(.journey-vignette-arrival) {
			margin-top: -10px;
			margin-bottom: -70px;
		}

		:global(.journey-vignette-daily) {
			margin-top: -10px;
			margin-bottom: -80px;
		}

		:global(.journey-vignette figcaption) {
			bottom: 4%;
		}

		.programs,
		:global(.mentor-section),
		.stories,
		.cta-minimal {
			padding-top: 90px;
			padding-bottom: 90px;
		}

		.journey-section-heading h2 {
			font-size: 42px;
		}

		:global(.mentor-minimal) {
			padding: 54px 12px;
		}
	}

	/* Reverted editorial experiment
	:global(body) {
		color: #343a35;
		background: #f4efe5;
		font-family: Georgia, 'Times New Roman', serif;
	}

	:global(body::before) {
		position: fixed;
		z-index: 100;
		inset: 0;
		background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 180 180' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='.16'/%3E%3C/svg%3E");
		content: '';
		opacity: 0.035;
		pointer-events: none;
	}

	.site-header {
		top: 0;
		width: min(1380px, calc(100% - 72px));
		height: 92px;
		padding: 0;
		border: 0;
		border-bottom: 1px solid rgba(52, 58, 53, 0.18);
		border-radius: 0;
		background: transparent;
		box-shadow: none;
		backdrop-filter: none;
	}

	.brand { gap: 7px; font-family: Arial, sans-serif; font-size: 15px; letter-spacing: 0.18em; text-transform: uppercase; }
	.brand small { padding-left: 9px; border-left: 1px solid rgba(52,58,53,.35); font-size: 8px; letter-spacing: .22em; }
	nav { gap: 38px; margin-left: auto; margin-right: 42px; }
	nav a { font-family: Arial, sans-serif; font-size: 11px; letter-spacing: .12em; text-transform: uppercase; }
	.desktop-cta { padding-bottom: 4px; border-bottom: 1px solid currentColor; font-family: Arial, sans-serif; font-size: 11px; letter-spacing: .12em; text-transform: uppercase; }

	.hero {
		min-height: 860px;
		background: #f4efe5;
	}
	.hero::before, .hero::after { display: none; }
	.hero-minimal {
		position: relative;
		display: block;
		width: 100%;
		height: min(100vh, 960px);
		min-height: 800px;
	}
	:global(.seattle-art) { position: absolute; z-index: 0; inset: 0; width: 100%; height: 100%; object-fit: cover; object-position: center; opacity: .96; }
	.hero-content { position: absolute; z-index: 2; top: 24%; left: max(36px, calc((100vw - 1280px) / 2)); max-width: 630px; text-align: left; }
	.hero-kicker { margin-bottom: 26px; font-family: Arial, sans-serif; font-size: 10px; font-weight: 700; letter-spacing: .2em; text-transform: uppercase; }
	h1 { margin-bottom: 28px; font-family: Georgia, 'Times New Roman', serif; font-size: clamp(66px, 7.4vw, 112px); font-weight: 400; line-height: .87; letter-spacing: -.055em; text-transform: none; }
	:global(.welcome-to-text) { font-size: 1em; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script { padding: 0; color: #526258; font-family: Georgia, 'Times New Roman', serif; font-size: 1em; font-style: italic; font-weight: 400; letter-spacing: -.055em; }
	.kawan-script::before, .kawan-script::after { display: none; }
	.hero-tagline { max-width: 470px; margin-bottom: 30px; color: #505851; font-family: Arial, sans-serif; font-size: 15px; line-height: 1.75; text-transform: none; }
	.hero-actions { justify-content: flex-start; margin-top: 0; }
	.button, :global(.button.gold) { min-height: 48px; padding: 0 20px; border: 1px solid #3f4d45; border-radius: 0; color: #f8f4eb; background: #3f4d45; box-shadow: 5px 5px 0 rgba(63,77,69,.13); font-family: Arial, sans-serif; font-size: 11px; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; }
	.button:hover, :global(.button.gold):hover { color: #f8f4eb; background: #2f3c35; box-shadow: 7px 7px 0 rgba(63,77,69,.12); }
	.hero-caption { position: absolute; z-index: 2; right: 4%; bottom: 5%; margin: 0; padding-left: 36px; color: #414a44; font-family: Arial, sans-serif; font-size: 10px; letter-spacing: .08em; }
	.hero-caption::before { position: absolute; top: 50%; left: 0; width: 24px; height: 1px; background: currentColor; content: ''; }
	.hero-caption span { margin-right: 10px; font-weight: 700; text-transform: uppercase; }

	.about, .programs, .stories, .cta-minimal, footer { background: #f4efe5; }
	.about, .programs, .stories { padding-top: 145px; padding-bottom: 145px; }
	.about::before, .about::after { display: none; }
	:global(.about-intro), .journey-section-heading { text-align: left; margin-left: 0; }
	:global(.about-intro) h2, .journey-section-heading h2, :global(.mentor-minimal) h2, .cta-content h2 { font-family: Georgia, 'Times New Roman', serif; font-weight: 400; letter-spacing: -.045em; }
	.about-eyebrow { color: #7b6251; font-family: Arial, sans-serif; font-size: 9px; letter-spacing: .22em; }
	:global(.journey-vignette) img, :global(.about-photo-crop) { border-radius: 0; filter: saturate(.72) sepia(.08); }
	:global(.about-photo-frame) { transform: rotate(1.5deg); }
	.about-grid { grid-template-columns: 1fr 1fr; gap: 0; border-top: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); }
	.about-card { min-height: 0; padding: 42px; border: 0; border-radius: 0; background: transparent; box-shadow: none; }
	.about-card + .about-card { border-left: 1px solid rgba(52,58,53,.22); }
	.about-card:hover, .program-card:hover { transform: none; box-shadow: none; }
	.program-grid.minimal { gap: 0; border-top: 1px solid rgba(52,58,53,.22); }
	.program-card { min-height: 310px; padding: 42px 34px; border: 0; border-right: 1px solid rgba(52,58,53,.22); border-bottom: 1px solid rgba(52,58,53,.22); border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	.card-icon { width: 34px; height: 34px; opacity: .62; }
	.program-card h3 { margin-top: auto; font-family: Georgia, 'Times New Roman', serif; font-size: 32px; font-weight: 400; }
	:global(.mentor-section) { background: #d9d3c4; }
	:global(.mentor-minimal) { border-color: rgba(52,58,53,.3); }
	.story-card { border: 0; border-radius: 0; background: transparent; box-shadow: none; backdrop-filter: none; }
	blockquote { font-family: Georgia, 'Times New Roman', serif; font-size: clamp(26px, 3vw, 40px); line-height: 1.42; }
	.student img { filter: grayscale(.35) sepia(.15); }
	.cta-minimal { border-top: 1px solid rgba(52,58,53,.18); }
	footer { border-top: 1px solid rgba(52,58,53,.22); }

	@media (max-width: 768px) {
		.site-header { width: calc(100% - 36px); height: 72px; }
		.desktop-cta { display: none; }
		nav.open { position: absolute; top: 72px; left: 0; display: flex; width: 100%; padding: 28px; flex-direction: column; gap: 24px; background: #f4efe5; border-bottom: 1px solid rgba(52,58,53,.2); }
		.menu-button { border-radius: 0; background: #3f4d45; }
		.hero-minimal { height: 820px; min-height: 820px; }
		:global(.seattle-art) { object-position: 62% center; opacity: .58; }
		.hero-content { top: 20%; right: 24px; left: 24px; }
		h1 { font-size: clamp(56px, 18vw, 82px); }
		.hero-tagline { max-width: 360px; }
		.hero-caption { right: 24px; bottom: 26px; }
		.about, .programs, .stories { padding-top: 90px; padding-bottom: 90px; }
		.about-grid { grid-template-columns: 1fr; }
		.about-card + .about-card { border-top: 1px solid rgba(52,58,53,.22); border-left: 0; }
		.program-card { min-height: 220px; border-left: 1px solid rgba(52,58,53,.22); }
		.story-card { padding: 20px 0; }
	}
	*/

	/* Cohesive watercolor section system with the cover intentionally unchanged */
	:global(main) {
		background: #fbf8f2;
	}

	.about,
	.programs,
	:global(.mentor-section),
	.stories,
	.cta-minimal {
		position: relative;
		z-index: 1;
		background: transparent;
	}

	.about {
		padding-top: 140px;
		background: #fbf8f2;
	}

	.about::before {
		display: block;
		position: absolute;
		top: 0;
		left: 50%;
		width: min(1180px, calc(100% - 64px));
		height: 1px;
		background: rgba(93, 102, 87, 0.14);
		content: '';
		transform: translateX(-50%);
	}

	:global(.about-intro),
	.belief-heading,
	.journey-section-heading {
		max-width: 720px;
		margin-right: auto;
		margin-left: auto;
		text-align: center;
	}

	.about-eyebrow,
	:global(.hand-note) {
		color: #7d5949;
		font-size: 10px;
		letter-spacing: 2.2px;
	}

	.illustration-band {
		position: relative;
		display: grid;
		min-height: 590px;
		grid-template-columns: minmax(280px, 0.8fr) minmax(420px, 1.2fr);
		gap: 70px;
		align-items: center;
		overflow: visible;
		margin: 68px 0 130px;
		padding: 68px 72px;
		border: 1px solid rgba(93, 102, 87, 0.1);
		border-radius: 2px;
		background: #f2eee4;
		box-shadow: 0 28px 70px rgba(76, 70, 59, 0.055);
	}

	.illustration-band::before {
		display: block;
		position: absolute;
		right: -7%;
		bottom: -20%;
		width: 46%;
		height: 58%;
		border: 0;
		background: rgba(180, 192, 171, 0.14);
		content: '';
		filter: blur(36px);
		transform: rotate(-5deg);
	}

	:global(.about-photo-frame),
	:global(.about-photo-frame):hover {
		z-index: 2;
		margin: 0;
		padding: 9px 9px 22px;
		border-radius: 1px;
		background: #fffdf8;
		box-shadow: 0 24px 54px rgba(72, 62, 52, 0.14);
		transform: rotate(1.2deg);
	}

	:global(.about-photo-crop) { border-radius: 0; }

	:global(.story-watercolor) {
		position: absolute !important;
		z-index: 1 !important;
		right: -9%;
		bottom: -27%;
		width: 54% !important;
		max-width: 680px;
		opacity: 0.72;
		filter: saturate(0.62) drop-shadow(0 14px 20px rgba(79, 72, 60, 0.06)) !important;
		pointer-events: none;
	}

	.belief-heading { margin-top: 40px; }
	.about-grid { max-width: 1080px; }
	.about-card,
	.about-card:first-child {
		position: relative;
		grid-template-columns: 180px 1fr;
		padding: 62px 30px;
	}
	.about-card::after {
		position: absolute;
		right: 4%;
		bottom: 18%;
		width: 92px;
		height: 52px;
		border-radius: 55% 45% 52% 48%;
		background: rgba(177, 189, 166, 0.18);
		content: '';
		filter: blur(10px);
		transform: rotate(-8deg);
	}
	.about-card:last-child::after { background: rgba(190, 133, 105, 0.12); transform: rotate(7deg); }

	.programs {
		overflow: hidden;
		padding-top: 150px;
		padding-bottom: 150px;
		background: #eef1e9;
	}
	.programs::before {
		position: absolute;
		top: -70px;
		left: -5%;
		width: 110%;
		height: 130px;
		border-radius: 50%;
		background: #fbf8f2;
		content: '';
	}
	:global(.section-watercolor) { margin: 0; pointer-events: none; }
	:global(.help-watercolor) {
		width: min(860px, 78vw);
		margin: -10px auto -150px;
		opacity: 0.58;
	}
	.program-grid.minimal { margin-top: 120px; }
	.program-card {
		border: 1px solid rgba(78, 92, 77, 0.1);
		border-radius: 2px;
		background: rgba(255, 253, 248, 0.8);
		box-shadow: 0 16px 42px rgba(62, 70, 60, 0.05);
		backdrop-filter: blur(8px);
	}
	.program-card:nth-child(2), .program-card:nth-child(2):hover { transform: none; }
	.card-icon { color: #697867; opacity: 0.65; }

	:global(.mentor-section) {
		overflow: hidden;
		padding: 150px 0 130px;
		background: #f6f1e7;
	}
	:global(.mentor-minimal) {
		display: grid;
		max-width: 1180px;
		grid-template-columns: 0.75fr 1.25fr;
		gap: 64px;
		align-items: center;
		padding: 60px 0;
		border-color: rgba(109, 92, 84, 0.16);
		text-align: left;
	}
	:global(.mentor-copy) { position: relative; z-index: 2; }
	:global(.mentor-minimal) h2 { margin-top: 10px; font-family: 'Fraunces', serif; font-size: clamp(46px, 5vw, 70px); line-height: 1; }
	:global(.mentor-minimal) p { max-width: 470px; font-size: 16px; line-height: 1.75; }
	:global(.community-watercolor) { margin: -80px -16% -90px -5%; opacity: 0.72; }
	:global(.involve-actions) { display: flex; align-items: center; gap: 28px; }
	.text-link { padding-bottom: 5px; border-bottom: 1px solid #78685e; color: #514843; font-size: 13px; font-weight: 650; }

	.stories { padding-top: 140px; padding-bottom: 140px; background: #fbf8f2; }
	.story-card { max-width: 820px; border-radius: 2px; background: #fffdf8; box-shadow: 0 24px 60px rgba(76, 70, 59, 0.07); }
	.cta-minimal { background: #e4e9df; }

	@media (max-width: 768px) {
		.about { padding-top: 92px; }
		.illustration-band { min-height: 0; grid-template-columns: 1fr; gap: 36px; margin: 44px 0 105px; padding: 38px 24px 100px; }
		:global(.story-watercolor) { right: -28%; bottom: -15%; width: 100% !important; opacity: .55; }
		.about-card, .about-card:first-child { grid-template-columns: 1fr; padding: 42px 4px; }
		.programs { padding-top: 105px; padding-bottom: 100px; }
		:global(.help-watercolor) { width: 135vw; margin: -10px 0 -70px -28vw; }
		.program-grid.minimal { margin-top: 70px; }
		:global(.mentor-section) { padding: 90px 0; }
		:global(.mentor-minimal) { grid-template-columns: 1fr; gap: 20px; padding: 30px 0; }
		:global(.community-watercolor) { width: 130%; margin: -20px -15% -35px; opacity: .62; }
		:global(.involve-actions) { align-items: flex-start; flex-direction: column; gap: 20px; }
		.stories { padding-top: 90px; padding-bottom: 90px; }
	}

	/* Small landmark accents */
	.illustration-band {
		min-height: 0;
		grid-template-columns: 1fr 1fr;
		gap: clamp(40px, 7vw, 96px);
		margin: 60px 0 120px;
		padding: clamp(44px, 6vw, 76px);
		background: #f4f0e7;
		box-shadow: none;
	}
	.illustration-band::before,
	.about-card::after,
	.programs::before { display: none; }
	.illustration-copy { padding-top: 70px; }
	:global(.about-photo-frame),
	:global(.about-photo-frame):hover { transform: rotate(.8deg); }
	:global(.section-accent) {
		display: block;
		width: 132px;
		height: 132px;
		object-fit: contain;
		opacity: .76;
		filter: saturate(.58);
		pointer-events: none;
	}
	:global(.story-accent) {
		position: absolute;
		top: -54px;
		left: -22px;
		width: 150px;
		height: 150px;
	}
	.belief-copy { position: relative; padding-right: 170px; }
	.belief-copy :global(.section-accent) {
		position: absolute;
		top: 50%;
		right: 4px;
		transform: translateY(-50%);
	}
	.programs {
		padding-top: 135px;
		background: #eef1e9;
	}
	:global(.heading-accent) {
		width: 150px;
		height: 120px;
		margin: 24px auto -18px;
	}
	.program-grid.minimal { margin-top: 64px; }
	.program-card { min-height: 280px; }
	:global(.mentor-minimal) {
		grid-template-columns: .9fr 1.1fr;
		gap: clamp(48px, 7vw, 100px);
	}
	:global(.mentor-copy) { padding-top: 72px; }
	:global(.involve-accent) {
		position: absolute;
		top: -72px;
		left: -18px;
		width: 138px;
		height: 138px;
	}
	:global(.involve-photo) {
		margin: 0;
		padding: 8px 8px 18px;
		background: #fffdf8;
		box-shadow: 0 20px 50px rgba(72,62,52,.12);
		transform: rotate(-.8deg);
	}
	:global(.involve-photo) img {
		width: 100%;
		aspect-ratio: 4 / 3;
		object-fit: cover;
		filter: saturate(.72) contrast(.96);
	}
	.stories :global(.heading-accent) { width: 168px; margin-bottom: -4px; }
	.story-card { box-shadow: none; border: 1px solid rgba(93,102,87,.11); }

	@media (max-width: 768px) {
		.illustration-band { grid-template-columns: 1fr; gap: 40px; padding: 36px 24px; }
		.illustration-copy { padding-top: 62px; }
		:global(.story-accent) { top: -60px; left: -12px; }
		.belief-copy { padding-right: 112px; }
		.belief-copy :global(.section-accent) { right: -14px; width: 108px; height: 108px; }
		:global(.heading-accent) { width: 126px; height: 104px; }
		:global(.mentor-copy) { padding-top: 66px; }
		:global(.involve-accent) { top: -74px; left: -8px; }
	}

	/* Modern editorial refinement and animated line art */
	:global(.reveal) {
		transform: translateY(28px);
		transition: opacity .8s cubic-bezier(.22, 1, .36, 1), transform .8s cubic-bezier(.22, 1, .36, 1);
	}
	:global(.line-accent) {
		display: block;
		width: 132px;
		height: 132px;
		color: #68766b;
		opacity: .68;
		stroke: currentColor;
		stroke-width: 1.35;
		stroke-linecap: round;
		stroke-linejoin: round;
		pointer-events: none;
	}
	:global(.line-accent) path {
		stroke-dasharray: 520;
		stroke-dashoffset: 520;
		transition: stroke-dashoffset 1.7s cubic-bezier(.22, 1, .36, 1) .15s;
	}
	:global(.line-accent .draw-late) { transition-delay: .48s; }
	:global(.visible) :global(.line-accent) path { stroke-dashoffset: 0; }
	:global(.story-accent) { position: absolute; top: -50px; left: -14px; width: 138px; height: 112px; }
	:global(.belief-copy :global(.line-accent)) { position: absolute; top: 50%; right: 10px; width: 126px; height: 126px; transform: translateY(-50%); }
	:global(.heading-accent) { width: 145px; height: 98px; margin: 28px auto -6px; }
	:global(.involve-accent) { position: absolute; top: -68px; left: -10px; width: 138px; height: 106px; }

	.about { padding-top: 156px; padding-bottom: 150px; }
	.illustration-band {
		padding: clamp(52px, 6vw, 78px);
		border-color: rgba(80, 93, 82, .11);
		background: #f8f5ee;
	}
	:global(.about-photo-frame),
	:global(.about-photo-frame):hover { box-shadow: 0 18px 42px rgba(58, 55, 48, .09); transform: none; }
	.about-card,
	.about-card:first-child { transition: padding .35s ease, background .35s ease; }
	.about-card:hover { padding-right: 38px; padding-left: 38px; background: rgba(238, 241, 233, .55); }

	.programs { padding-top: 145px; padding-bottom: 150px; background: #f0f2ec; }
	.program-grid.minimal {
		display: grid;
		grid-template-columns: repeat(6, minmax(0, 1fr));
		gap: 16px;
		max-width: 1180px;
		margin: 72px auto 0;
	}
	.program-card {
		grid-column: span 2;
		min-height: 390px;
		gap: 18px;
		padding: 34px;
		border: 1px solid rgba(76, 91, 78, .12);
		border-radius: 3px;
		background: rgba(255, 255, 252, .72);
		box-shadow: none;
		backdrop-filter: none;
		transition: transform .35s cubic-bezier(.22,1,.36,1), border-color .35s ease, box-shadow .35s ease;
	}
	.program-card:nth-child(4) { grid-column: 2 / span 2; }
	.program-card:hover {
		transform: translateY(-6px);
		border-color: rgba(76, 91, 78, .24);
		box-shadow: 0 18px 42px rgba(58, 68, 59, .07);
	}
	.card-icon { width: 42px; height: 42px; margin-bottom: 8px; color: #68786b; }
	.card-icon svg { stroke: currentColor; stroke-width: 1.45; stroke-linecap: round; stroke-linejoin: round; }
	.program-card h3 { margin-top: 0; font-family: 'Fraunces', serif; font-size: 28px; font-weight: 600; letter-spacing: -.7px; }
	.program-card > p { margin: 0; color: #686965; font-size: 14px; line-height: 1.65; }
	.program-card ul { display: flex; flex-wrap: wrap; gap: 7px; margin: 2px 0 8px; padding: 0; list-style: none; }
	.program-card li { padding: 6px 9px; border: 1px solid rgba(104,120,107,.13); border-radius: 999px; color: #666d65; background: rgba(238,241,233,.55); font-size: 10px; letter-spacing: .02em; }
	.program-card a { margin-top: auto; font-size: 12px; }

	:global(.mentor-section) { padding-top: 145px; padding-bottom: 145px; }
	:global(.involve-photo) { box-shadow: 0 18px 46px rgba(58,55,48,.1); transform: none; }
	.story-card { transition: transform .35s ease, border-color .35s ease; }
	.story-card:hover { transform: translateY(-3px); border-color: rgba(93,102,87,.2); }
	.button, .text-link, nav a { transition-duration: .3s; }

	@media (max-width: 900px) {
		.program-grid.minimal { grid-template-columns: repeat(2, minmax(0, 1fr)); }
		.program-card, .program-card:nth-child(4) { grid-column: auto; }
		.program-card:last-child { grid-column: 1 / -1; }
	}
	@media (max-width: 620px) {
		.program-grid.minimal { grid-template-columns: 1fr; }
		.program-card, .program-card:last-child { grid-column: auto; min-height: 340px; }
		.belief-copy { padding-right: 94px; }
		:global(.belief-copy :global(.line-accent)) { right: -14px; width: 98px; height: 98px; }
	}
	@media (prefers-reduced-motion: reduce) {
		:global(html) { scroll-behavior: auto; }
		:global(.reveal), :global(.reveal.visible) { opacity: 1; transform: none; transition: none; }
		:global(.line-accent) path { stroke-dashoffset: 0; transition: none; }
		.program-card, .story-card, .button { transition: none; }
	}

	.header-logo {
		display: block;
		width: 58px;
		height: 58px;
		object-fit: contain;
	}
	.site-header > .brand {
		align-self: stretch;
		align-items: center;
		line-height: 0;
	}
	@media (max-width: 768px) {
		.header-logo { width: 48px; height: 48px; }
	}

	/* Reverted community first homepage styles
	.hero {
		min-height: 860px;
		background: #f5efe5;
	}
	.hero::before,
	.hero::after { display: block; }
	.hero::before {
		right: auto;
		bottom: -80px;
		left: -70px;
		width: 280px;
		height: 280px;
		background: rgba(174, 188, 162, .2);
		filter: blur(2px);
	}
	.hero::after {
		top: 18%;
		right: 3%;
		left: auto;
		width: 100px;
		height: 64px;
		border: 1px solid rgba(177, 110, 78, .2);
		background: transparent;
		transform: rotate(-8deg);
	}
	.hero-minimal {
		display: grid;
		height: auto;
		min-height: 860px;
		grid-template-columns: minmax(0, .9fr) minmax(460px, 1.1fr);
		gap: clamp(48px, 7vw, 110px);
		align-items: center;
		padding-top: 128px;
		padding-bottom: 72px;
	}
	.hero-content { max-width: 600px; text-align: left; }
	.hero-kicker {
		margin: 0 0 12px;
		color: #886653;
		font-size: 11px;
		font-weight: 750;
		letter-spacing: .22em;
		text-transform: uppercase;
	}
	.hero h1 { margin: 0; font-size: clamp(78px, 9vw, 132px); line-height: .86; text-transform: none; }
	.hero .kawan-script { padding: 0; color: #3d4d43; font-style: normal; letter-spacing: -.07em; text-transform: uppercase; }
	.hero .kawan-script::before { display: none; }
	.hero-statement {
		margin: 26px 0 14px;
		color: #4e4944;
		font-family: 'Fraunces', serif;
		font-size: clamp(27px, 3vw, 40px);
		font-weight: 500;
		line-height: 1.15;
		letter-spacing: -.03em;
	}
	.hero-tagline { max-width: 520px; margin: 0 0 30px; color: #69645f; font-size: 16px; line-height: 1.75; text-transform: none; }
	.hero-actions { justify-content: flex-start; margin: 0; }
	:global(.hero-photo) {
		position: relative;
		z-index: 2;
		margin: 0;
		padding: 10px 10px 28px;
		border-radius: 22px;
		background: #fffdf9;
		box-shadow: 0 28px 70px rgba(71, 60, 49, .16);
		transform: rotate(1.2deg);
	}
	:global(.hero-photo)::before {
		position: absolute;
		z-index: -1;
		top: -18px;
		right: -18px;
		width: 88px;
		height: 88px;
		border-radius: 50%;
		background: #c98262;
		content: '';
		opacity: .32;
	}
	:global(.hero-photo) img { width: 100%; aspect-ratio: 4 / 3; border-radius: 15px; object-fit: cover; filter: saturate(.82) contrast(.97); }
	:global(.hero-photo figcaption) { padding: 14px 8px 0; color: #746b63; font-family: 'Fraunces', serif; font-size: 14px; font-style: italic; }

	.feature-strip {
		position: relative;
		z-index: 4;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 18px;
		padding-top: 72px;
		padding-bottom: 96px;
		background: #fbf8f2;
	}
	.feature-card {
		position: relative;
		min-height: 290px;
		padding: 36px;
		border-radius: 18px;
		background: #fffdf9;
		box-shadow: 0 14px 36px rgba(69, 65, 56, .07);
		transition: transform .35s cubic-bezier(.22,1,.36,1), box-shadow .35s ease;
	}
	.feature-card:nth-child(2) { background: #edf0e8; }
	.feature-card:nth-child(3) { background: #f4e8df; }
	.feature-card:hover { transform: translateY(-6px); box-shadow: 0 20px 44px rgba(69,65,56,.1); }
	.feature-icon { width: 44px; height: 44px; color: #657467; }
	.feature-icon svg { width: 100%; height: 100%; stroke: currentColor; stroke-width: 1.5; stroke-linecap: round; stroke-linejoin: round; }
	.feature-number { position: absolute; top: 38px; right: 36px; color: #b06f52; font-family: 'Fraunces', serif; font-size: 14px; }
	.feature-card h2 { margin: 52px 0 14px; font-family: 'Fraunces', serif; font-size: 30px; font-weight: 600; letter-spacing: -.04em; }
	.feature-card > p:last-child { margin: 0; color: #6b6862; font-size: 14px; line-height: 1.7; }

	.community-banner { position: relative; overflow: hidden; width: calc(100% - 64px); max-width: 1380px; height: min(72vw, 720px); margin: 0 auto; border-radius: 24px; }
	.community-banner img { width: 100%; height: 100%; object-fit: cover; filter: saturate(.78) contrast(.96); }
	.community-banner::after { position: absolute; inset: 45% 0 0; background: linear-gradient(transparent, rgba(29,35,31,.72)); content: ''; }
	.community-caption { position: absolute; z-index: 2; right: 7%; bottom: 8%; left: 7%; display: flex; align-items: end; justify-content: space-between; gap: 30px; color: white; }
	.community-caption span { font-size: 11px; font-weight: 750; letter-spacing: .2em; text-transform: uppercase; }
	.community-caption p { max-width: 520px; margin: 0; font-family: 'Fraunces', serif; font-size: clamp(28px, 4vw, 52px); line-height: 1.05; text-align: right; }

	.about { padding-top: 150px; }
	.illustration-band {
		grid-template-columns: 1fr .72fr;
		align-items: end;
		max-width: 1060px;
		margin-right: auto;
		margin-left: auto;
		padding: 0 0 100px;
		border: 0;
		border-bottom: 1px solid rgba(90, 94, 83, .16);
		border-radius: 0;
		background: transparent;
	}
	.illustration-copy { padding-top: 60px; }
	.story-pullquote { margin: 0; padding: 34px; border-radius: 18px; color: #556057; background: #edf0e8; font-family: 'Fraunces', serif; font-size: clamp(24px, 3vw, 38px); font-style: italic; line-height: 1.25; transform: rotate(-1deg); }
	.belief-heading { margin-top: 110px; }
	.about-card, .about-card:first-child { border-color: rgba(90,94,83,.13); }

	.programs { background: #edf0e8; }
	.program-card { border-radius: 16px; background: rgba(255,253,248,.82); }
	.events { padding-top: 145px; padding-bottom: 145px; background: #fbf8f2; }
	.events-heading { display: grid; grid-template-columns: 1.2fr .8fr; gap: 80px; align-items: end; max-width: 1120px; margin: 0 auto 64px; }
	.events-heading h2 { max-width: 680px; margin: 10px 0 0; font-family: 'Fraunces', serif; font-size: clamp(46px, 5vw, 68px); font-weight: 600; line-height: 1.04; letter-spacing: -.045em; }
	.events-heading > p { margin: 0; color: #706b65; font-size: 15px; line-height: 1.75; }
	.event-list { max-width: 1120px; margin: 0 auto; border-top: 1px solid rgba(83,92,82,.16); }
	.event-item { display: grid; grid-template-columns: 50px 1fr 1.2fr auto; gap: 30px; align-items: center; padding: 34px 4px; border-bottom: 1px solid rgba(83,92,82,.16); }
	.event-item > span { color: #b17154; font-family: 'Fraunces', serif; font-size: 14px; }
	.event-item div p { margin: 0 0 4px; color: #8a6654; font-size: 9px; font-weight: 750; letter-spacing: .18em; text-transform: uppercase; }
	.event-item h3 { margin: 0; font-family: 'Fraunces', serif; font-size: 27px; font-weight: 600; }
	.event-item > p { margin: 0; color: #706c66; font-size: 14px; line-height: 1.6; }
	.event-item a { padding-bottom: 5px; border-bottom: 1px solid currentColor; color: #4f5c52; font-size: 12px; font-weight: 650; white-space: nowrap; }
	:global(.mentor-section) { background: #f3e9df; }
	.stories { background: #fbf8f2; }
	.cta-minimal { background: #dfe6dc; }

	@media (max-width: 900px) {
		.hero-minimal { min-height: auto; grid-template-columns: 1fr; gap: 54px; padding-top: 130px; padding-bottom: 80px; }
		:global(.hero-photo) { width: min(620px, 92%); justify-self: center; }
		:global(.hero-photo) img { aspect-ratio: 4 / 3; }
		.feature-strip { grid-template-columns: 1fr; }
		.feature-card { min-height: 245px; }
		.events-heading { grid-template-columns: 1fr; gap: 28px; }
		.event-item { grid-template-columns: 36px 1fr; }
		.event-item > p, .event-item > a { grid-column: 2; }
	}
	@media (max-width: 620px) {
		.hero h1 { font-size: clamp(68px, 23vw, 96px); }
		.hero-statement { font-size: 29px; }
		:global(.hero-photo) { width: 100%; padding: 7px 7px 22px; border-radius: 16px; transform: none; }
		:global(.hero-photo) img { border-radius: 11px; }
		.feature-strip { padding-top: 54px; padding-bottom: 72px; }
		.community-banner { width: calc(100% - 24px); height: 72vh; max-height: 620px; border-radius: 16px; }
		.community-caption { align-items: flex-start; flex-direction: column; }
		.community-caption p { text-align: left; }
		.illustration-band { grid-template-columns: 1fr; padding-bottom: 78px; }
		.story-pullquote { margin-top: 10px; }
		.events { padding-top: 100px; padding-bottom: 100px; }
		.event-item { gap: 16px; padding: 28px 0; }
	}

	Seattle outline hero
	.hero-minimal {
		display: flex;
		min-height: 900px;
		align-items: center;
		justify-content: flex-start;
		padding-top: 120px;
		padding-bottom: 260px;
	}
	.hero-content {
		z-index: 3;
		max-width: 690px;
		margin: 0 auto;
		text-align: center;
	}
	.hero-actions { justify-content: center; }
	.seattle-outline {
		position: absolute;
		z-index: 1;
		bottom: 0;
		left: 50%;
		width: 100vw;
		height: auto;
		max-width: none;
		opacity: .78;
		filter: saturate(.62) contrast(.94);
		transform: translateX(-50%);
		pointer-events: none;
	}
	@media (max-width: 768px) {
		.hero-minimal { min-height: 820px; padding-top: 120px; padding-bottom: 220px; }
		.seattle-outline { width: 160vw; opacity: .68; }
	}
	*/
	.hero-statement {
		margin: 0 0 10px;
		color: #4f4945;
		font-family: 'Fraunces', serif;
		font-size: clamp(24px, 2.6vw, 34px);
		font-weight: 600;
		line-height: 1.2;
		letter-spacing: -0.8px;
	}
	.hero-statement + .hero-tagline {
		max-width: 590px;
		margin-right: auto;
		margin-bottom: 34px;
		margin-left: auto;
		font-size: 17px;
		line-height: 1.65;
		text-transform: none;
	}
	.footer-identity {
		display: inline-flex;
		align-items: center;
		gap: 16px;
	}
	.footer-identity img {
		width: 76px;
		height: 76px;
		object-fit: contain;
	}
	.footer-identity > span {
		display: flex;
		flex-direction: column;
		gap: 3px;
	}
	.footer-identity strong {
		color: var(--ink);
		font-family: 'Manrope', sans-serif;
		font-size: 20px;
		letter-spacing: .08em;
	}
	.footer-identity small {
		color: var(--muted);
		font-size: 8px;
		font-weight: 700;
		letter-spacing: .24em;
	}

	/* Human, photo led About section */
	:global(.about-intro) {
		margin-bottom: 28px;
	}
	.illustration-band {
		min-height: 0;
		grid-template-columns: minmax(280px, .75fr) minmax(520px, 1.25fr);
		gap: clamp(44px, 6vw, 84px);
		align-items: center;
		margin-top: 20px;
		padding: 58px 58px 48px;
	}
	.illustration-copy {
		padding-top: 0;
	}
	.illustration-copy .story-lead {
		max-width: 510px;
		margin: 0 0 28px;
		color: #464541;
		font-family: 'Fraunces', serif;
		font-size: clamp(26px, 2.7vw, 39px);
		font-weight: 500;
		line-height: 1.22;
		letter-spacing: -1px;
	}
	.story-lead strong {
		display: inline;
		font-weight: 650;
	}
	.illustration-copy > p:not(.story-lead) {
		max-width: 470px;
		font-size: 15px;
		line-height: 1.78;
	}
	.about-photo-frame,
	.about-photo-frame:hover {
		position: relative;
		margin: 0;
		padding: 9px 9px 16px;
		border: 1px solid rgba(100, 88, 76, .08);
		border-radius: 2px;
		background: #fffdf8;
		box-shadow: 0 22px 52px rgba(67, 57, 49, .13);
		transform: rotate(.7deg);
	}
	.about-photo-frame::before {
		position: absolute;
		top: -13px;
		left: 50%;
		width: 82px;
		height: 25px;
		background: rgba(223, 210, 188, .72);
		content: '';
		transform: translateX(-50%) rotate(-1.5deg);
	}
	.about-photo-crop {
		position: relative;
		aspect-ratio: 3 / 2;
		overflow: hidden;
		border-radius: 0;
	}
	.about-photo-crop img {
		position: static;
		width: 100%;
		height: 100%;
		max-width: 100%;
		object-fit: cover;
		filter: saturate(.84) contrast(.97);
		transform: none;
	}
	@media (max-width: 900px) {
		.illustration-band { grid-template-columns: 1fr; padding: 46px 36px 38px; }
		.about-photo-frame { width: min(680px, 100%); }
	}
	@media (max-width: 620px) {
		:global(.about-intro) { margin-bottom: 18px; }
		.illustration-band { gap: 34px; margin-top: 10px; padding: 36px 20px 28px; }
		.illustration-copy .story-lead { font-size: 27px; }
	}

	/* Typography led Vision and Mission */
	.belief-section {
		position: relative;
		z-index: 0;
		margin-top: 130px;
		padding: 118px 0 128px;
	}
	.belief-section::before {
		position: absolute;
		z-index: -1;
		inset: 0 50%;
		width: 100vw;
		background: #f4f6f1;
		content: '';
		transform: translateX(-50%);
	}
	.belief-heading {
		margin: 0 0 86px;
		text-align: left;
	}
	.belief-heading h2 {
		max-width: 720px;
		font-size: clamp(52px, 6vw, 78px);
		line-height: .98;
	}
	.about-grid {
		display: grid;
		max-width: 1160px;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: clamp(70px, 10vw, 150px);
		margin: 0 auto;
	}
	.about-card,
	.about-card:first-child,
	.about-card:last-child {
		display: block;
		min-height: 0;
		padding: 0;
		border: 0;
		background: transparent;
		box-shadow: none;
	}
	.about-card:hover,
	.about-card:first-child:hover,
	.about-card:last-child:hover {
		padding: 0;
		background: transparent;
		box-shadow: none;
		transform: none;
	}
	.belief-label {
		display: block;
		margin-bottom: 34px;
	}
	.belief-label .about-label {
		display: inline-block;
		position: relative;
		padding-bottom: 9px;
		color: #7d5949;
		font-size: 10px;
		letter-spacing: .22em;
	}
	.belief-label .about-label::after {
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		height: 1px;
		background: #bd7658;
		content: '';
		transform: scaleX(0);
		transform-origin: left;
		transition: transform 1s cubic-bezier(.22, 1, .36, 1) .35s;
	}
	:global(.about-card.visible) .about-label::after {
		transform: scaleX(1);
	}
	.belief-copy {
		padding: 0;
	}
	.belief-copy h3 {
		max-width: 540px;
		margin: 0 0 32px;
		color: #39423c;
		font-family: 'Fraunces', serif;
		font-size: clamp(46px, 5.2vw, 70px);
		font-weight: 580;
		line-height: 1.02;
		letter-spacing: -.055em;
	}
	.belief-copy .about-description {
		max-width: 490px;
		color: #666c65;
		font-size: 16px;
		line-height: 1.78;
	}
	@media (max-width: 800px) {
		.belief-section { margin-top: 90px; padding: 88px 0 98px; }
		.belief-heading { margin-bottom: 64px; }
		.about-grid { grid-template-columns: 1fr; gap: 86px; }
		.belief-copy h3 { font-size: clamp(44px, 12vw, 62px); }
	}
	@media (prefers-reduced-motion: reduce) {
		.belief-label .about-label::after { transform: scaleX(1); transition: none; }
	}

	/* Unified editorial About section */
	.about {
		padding-top: 150px;
	}
	.illustration-band {
		grid-template-columns: minmax(340px, .85fr) minmax(520px, 1.15fr);
		gap: clamp(60px, 8vw, 110px);
		align-items: center;
		margin: 0;
		padding: 0 0 145px;
		border: 0;
		border-radius: 0;
		background: transparent;
		box-shadow: none;
	}
	.illustration-copy h2 {
		max-width: 570px;
		margin: 12px 0 22px;
		color: #3d403c;
		font-family: 'Fraunces', serif;
		font-size: clamp(52px, 6vw, 76px);
		font-weight: 600;
		line-height: .98;
		letter-spacing: -.055em;
	}
	.illustration-copy .story-lead {
		margin-bottom: 26px;
		font-size: clamp(24px, 2.45vw, 34px);
		line-height: 1.27;
	}
	.about-photo-frame,
	.about-photo-frame:hover {
		padding: 7px;
		border: 1px solid rgba(78, 75, 68, .08);
		border-radius: 12px;
		background: #fff;
		box-shadow: 0 20px 50px rgba(59, 56, 49, .1);
		transform: none;
	}
	.about-photo-frame::before {
		display: none;
	}
	.about-photo-crop {
		aspect-ratio: 4 / 3;
		border-radius: 7px;
	}
	.about-photo-crop img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center 46%;
		transform: scale(1.18);
	}
	@media (max-width: 900px) {
		.about { padding-top: 100px; }
		.illustration-band { grid-template-columns: 1fr; gap: 54px; padding-bottom: 105px; }
		.illustration-copy { max-width: 650px; }
		.about-photo-frame { width: 100%; }
	}
	@media (max-width: 620px) {
		.illustration-band { gap: 42px; padding: 0 0 84px; }
		.illustration-copy h2 { font-size: 52px; }
		.about-photo-frame { padding: 5px; border-radius: 9px; }
	}

	/* Unified KAWAN design system */
	:global(body) {
		color: #343a35;
		background: #faf7f0;
		font-family: 'Manrope', sans-serif;
	}
	h1, h2, h3, blockquote,
	.hero-statement,
	.illustration-copy h2,
	.belief-heading h2,
	.belief-copy h3,
	.journey-section-heading h2,
	.program-card h3,
	.cta-content h2 {
		font-family: 'Fraunces', serif;
	}
	.about-eyebrow, .about-label {
		color: #8a6250;
		font-family: 'Manrope', sans-serif;
		font-size: 10px;
		font-weight: 700;
		letter-spacing: .2em;
		text-transform: uppercase;
	}
	.button, :global(.button.gold) {
		min-height: 50px;
		padding: 0 22px;
		border: 0;
		border-radius: 6px;
		color: #fffdf8;
		background: #46564b;
		box-shadow: none;
		font-family: 'Manrope', sans-serif;
		font-size: 12px;
		font-weight: 700;
		letter-spacing: .04em;
	}
	.button:hover, :global(.button.gold):hover { background: #35433a; box-shadow: none; transform: translateY(-2px); }

	.hero {
		position: relative;
		overflow: hidden;
		min-height: 790px;
		background: #f4eee4;
	}
	.hero::before, .hero::after { display: none; }
	.hero-minimal {
		position: relative;
		display: flex;
		min-height: 790px;
		align-items: center;
		justify-content: center;
		padding-top: 142px;
		padding-bottom: 96px;
	}
	.hero-content {
		position: relative;
		z-index: 2;
		max-width: 760px;
		text-align: center;
	}
	.hero-content > * {
		opacity: 0;
		animation: hero-copy-in .75s cubic-bezier(.2,.7,.2,1) both;
	}
	.hero-content .hero-kicker { animation-delay: .08s; }
	.hero-content h1 { animation-delay: .2s; }
	.hero-content .hero-statement { animation-delay: .34s; }
	.hero-content .hero-tagline { animation-delay: .48s; }
	.hero-content .hero-actions { animation-delay: .62s; }
	.hero-kicker { margin: 0 0 10px; color: #846351; font-size: 11px; font-weight: 700; letter-spacing: .2em; text-transform: uppercase; }
	.hero h1 { margin: 0; font-size: clamp(88px, 12vw, 152px); line-height: .85; letter-spacing: -.065em; text-transform: none; }
	.hero .kawan-script { padding: 0; color: #405047; font-family: 'Fraunces', serif; font-size: 1em; font-style: normal; font-weight: 650; letter-spacing: -.065em; text-transform: uppercase; }
	.hero .kawan-script::before { display: none; }
	.hero-statement { margin: 32px 0 13px; font-size: clamp(30px, 3.3vw, 43px); font-weight: 550; letter-spacing: -.035em; }
	.hero-statement + .hero-tagline { max-width: 620px; margin: 0 auto 32px; color: #66635e; font-size: 15px; line-height: 1.75; }
	.hero-actions { justify-content: center; margin: 0; }
	.hero-illustrations {
		position: absolute;
		z-index: 1;
		inset: 92px 0 18px;
		pointer-events: none;
	}
	.hero-illustration {
		--hero-art-opacity: .96;
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		object-fit: contain;
		opacity: calc(var(--hero-art-opacity) * var(--hero-scroll-fade));
		pointer-events: none;
		mask-image: linear-gradient(90deg, #000, #000);
		mask-repeat: no-repeat;
		mask-size: 0% 100%;
		animation: illustration-reveal .85s cubic-bezier(.2,.7,.2,1) forwards;
	}
	.illustration-space-needle { clip-path: inset(0 50% 50% 0); animation-delay: .72s; }
	.illustration-board-game { clip-path: inset(0 0 50% 50%); animation-delay: .9s; }
	.illustration-water-taxi { clip-path: inset(50% 50% 0 0); animation-delay: 1.08s; }
	.illustration-hiking { clip-path: inset(50% 0 0 50%); animation-delay: 1.26s; }
	.hero-actions .button { transition: background .25s ease, box-shadow .25s ease, transform .25s ease; }
	.hero-actions .button span { display: inline-block; transition: transform .25s ease; }
	.hero-actions .button:hover { background: #35433a; box-shadow: 0 8px 18px rgba(48,60,51,.16); transform: translateY(-2px); }
	.hero-actions .button:hover span { transform: translate(4px, -4px); }
	@keyframes hero-copy-in { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: none; } }
	@keyframes illustration-reveal { to { mask-size: 100% 100%; } }

	.about { padding-top: 145px; padding-bottom: 0; background: #faf7f0; }
	.illustration-band { gap: clamp(62px, 8vw, 110px); padding-bottom: 145px; }
	.about-photo-frame, .about-photo-frame:hover {
		border-radius: 10px;
		box-shadow: 0 20px 52px rgba(55,52,46,.1);
		transform: none;
	}
	.illustration-copy > p:not(.story-lead) { font-weight: 500; }
	.illustration-copy > p strong { font-weight: 600; }

	.belief-section { margin-top: 0; padding: 128px 0 136px; }
	.belief-section::before { background: #f1f4ee; }
	.belief-heading { margin-bottom: 88px; }
	.about-grid { display: block; max-width: 1000px; }
	.about-card, .about-card:first-child, .about-card:last-child { display: grid; grid-template-columns: 210px 1fr; gap: 60px; padding: 58px 0; border-top: 1px solid rgba(67,79,69,.15); }
	.about-card:last-child { border-bottom: 1px solid rgba(67,79,69,.15); }
	.about-card:hover, .about-card:first-child:hover, .about-card:last-child:hover { padding: 58px 0; }
	.belief-label { margin: 8px 0 0; }
	.belief-copy h3 { max-width: 650px; font-size: clamp(48px, 5.4vw, 72px); }

	.programs { padding-top: 145px; padding-bottom: 150px; background: #faf7f0; }
	.journey-section-heading { max-width: 760px; }
	.program-grid.minimal { gap: 14px; }
	.program-card {
		min-height: 380px;
		padding: 34px;
		border: 1px solid rgba(64,77,66,.12);
		border-radius: 7px;
		background: #fffdf8;
		box-shadow: none;
		backdrop-filter: none;
	}
	.program-card:hover { border-color: rgba(64,77,66,.25); box-shadow: 0 14px 34px rgba(58,65,58,.06); }
	.program-card li { border-radius: 4px; }

	.community-photo-break {
		position: relative;
		overflow: hidden;
		width: min(1400px, calc(100% - 48px));
		height: clamp(430px, 64vw, 720px);
		margin: 0 auto;
		border-radius: 10px;
	}
	.community-photo-break img { width: 100%; height: 100%; object-fit: cover; object-position: center; filter: saturate(.84) contrast(.97); }
	.community-photo-break::after { position: absolute; inset: 55% 0 0; background: linear-gradient(transparent, rgba(29,36,31,.64)); content: ''; }
	.community-photo-break p { position: absolute; z-index: 2; right: 7%; bottom: 7%; max-width: 620px; margin: 0; color: white; font-family: 'Fraunces', serif; font-size: clamp(32px, 4.6vw, 64px); line-height: 1.05; text-align: right; }

	.stories { padding-top: 145px; padding-bottom: 145px; background: #faf7f0; }
	.story-card { border: 1px solid rgba(64,77,66,.11); border-radius: 8px; box-shadow: none; }
	.student img { filter: saturate(.82); }

	.cta-minimal { padding: 150px 0; background: #eef2eb; }
	.cta-content { max-width: 820px; margin: 0 auto; }
	.cta-content h2 { margin: 12px 0 24px; font-size: clamp(56px, 7vw, 88px); line-height: .98; }
	.cta-content > p:not(.about-eyebrow) { max-width: 590px; margin: 0 auto 34px; color: #666b65; font-size: 16px; line-height: 1.75; }
	.cta-actions { display: flex; align-items: center; justify-content: center; gap: 28px; }
	.text-link { font-family: 'Manrope', sans-serif; }

	footer { background: #e5e9e1; }
	@media (max-width: 900px) {
		.hero, .hero-minimal { min-height: 740px; }
		.hero-minimal { padding-top: 135px; padding-bottom: 84px; }
		.hero-illustrations { inset: 112px -10% 20px; }
		.hero-illustration { width: 100%; max-width: none; }
		.about-card, .about-card:first-child, .about-card:last-child { grid-template-columns: 1fr; gap: 28px; }
	}
	@media (max-width: 620px) {
		.hero, .hero-minimal { min-height: 700px; }
		.hero-minimal { padding-top: 124px; padding-bottom: 72px; }
		.hero h1 { font-size: clamp(72px, 24vw, 102px); }
		.hero-content { max-width: 94%; }
		.hero-statement { font-size: 30px; }
		.hero-tagline { max-width: 340px; }
		.hero-illustrations { inset: 106px -36% 10px; }
		.hero-illustration { --hero-art-opacity: .7; width: 100%; }
		.about { padding-top: 100px; }
		.community-photo-break { width: calc(100% - 24px); height: 62vh; border-radius: 7px; }
		.community-photo-break p { right: 8%; bottom: 7%; left: 8%; text-align: left; }
		.cta-actions { align-items: stretch; flex-direction: column; }
	}
	@media (prefers-reduced-motion: reduce) {
		.hero-content > *, .hero-illustration { opacity: 1; animation: none; mask-size: 100% 100%; }
	}
</style>
