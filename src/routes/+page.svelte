<script lang="ts">
	import { onMount } from 'svelte';
	import { base } from '$app/paths';

	const programs = [
		{
			number: '01',
			title: 'Plan your path',
			color: 'sage'
		},
		{
			number: '02',
			title: 'Prepare to go',
			color: 'sand'
		},
		{
			number: '03',
			title: 'Belong & thrive',
			color: 'coral'
		}
	];

	const stories = [
		{
			quote:
				'My mentor helped me turn a confusing process into a clear plan. I arrived feeling prepared—not alone.',
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
					if (entry.isIntersecting) entry.target.classList.add('visible');
				}
			},
			{ threshold: 0.12 }
		);

		document.querySelectorAll('.reveal').forEach((element) => observer.observe(element));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>Kawan — Your journey. Our guidance.</title>
</svelte:head>

<header class="site-header">
	<a class="brand" href="#top" aria-label="Kawan home">
		<span class="brand-mark" aria-hidden="true">
			<svg viewBox="0 0 44 44" fill="none">
				<path d="M5 27.5c7-12 16-15 33-12-7.5 2.8-11 8-12.2 15.2C20 24.8 13.2 24.5 5 27.5Z" fill="currentColor" />
				<path d="M10 32c8-5 15-5.8 24-3.2" stroke="currentColor" stroke-width="2.7" stroke-linecap="round" />
			</svg>
		</span>
		<span>Kawan</span>
	</a>

	<nav class:open={menuOpen} aria-label="Primary navigation">
		<a href="#about" onclick={() => (menuOpen = false)}>About</a>
		<a href="#programs" onclick={() => (menuOpen = false)}>How we help</a>
		<a href="#stories" onclick={() => (menuOpen = false)}>Stories</a>
	</nav>

	<a class="button small desktop-cta" href="#connect">Get guidance <span>↗</span></a>
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
	<section class="hero">
		<div class="hero-minimal">
			<div class="hero-content reveal visible">
				<h1><span class="welcome-to-text">welcome to</span> <span class="kawan-script">kawan</span></h1>
				<p class="hero-tagline">guidance for international students in seattle</p>
				<div class="hero-actions">
					<a class="button" href="#programs">let's start <span>↗</span></a>
				</div>
			</div>
			<div class="hero-shape"></div>
		</div>
	</section>

	<section class="about section-wrap" id="about">
		<div class="about-intro reveal">
			<p class="about-eyebrow">who we are</p>
		</div>
		<div class="about-grid reveal">
			<article class="about-card">
				<p class="about-label">definition</p>
				<h3>kawan</h3>
				<p class="about-description">"friend" or "companion" in indonesian — someone who walks beside you when everything feels new.</p>
			</article>
			<article class="about-card">
				<p class="about-label">our vision</p>
				<h3>make belonging feel possible</h3>
				<p class="about-description">we imagine a seattle where international students are welcomed, understood, and fully part of the community from day one.</p>
			</article>
			<article class="about-card">
				<p class="about-label">our mission</p>
				<h3>build connection, confidence, and care</h3>
				<p class="about-description">through mentoring, friendship, and practical guidance, we help students settle in, thrive, and feel at home where they study.</p>
			</article>
		</div>
	</section>

	<section class="programs section-wrap" id="programs">
		<div class="program-grid minimal">
			{#each programs as program, index}
				<article class="program-card {program.color} reveal" style={`--delay: ${index * 90}ms`}>
					<div class="card-icon">
						{#if index === 0}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<circle cx="20" cy="20" r="14" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{:else if index === 1}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<rect x="10" y="10" width="20" height="20" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{:else}
							<svg viewBox="0 0 40 40" fill="none" aria-hidden="true">
								<path d="M20 31s-11-5.8-11-13.3A6.7 6.7 0 0 1 20 12.5a6.7 6.7 0 0 1 11 5.2C31 25.2 20 31 20 31Z" stroke="currentColor" stroke-width="1.8" />
							</svg>
						{/if}
					</div>
					<h3>{program.title}</h3>
					<a href="#connect" aria-label={`Explore ${program.title}`}>Learn more <span>↗</span></a>
				</article>
			{/each}
		</div>
	</section>

	<section class="mentor-section" id="connect">
		<div class="section-wrap">
			<div class="mentor-minimal reveal">
				<div class="mentor-dot"></div>
				<h2>Meet a mentor</h2>
				<p>Free guidance from someone who's been where you are</p>
				<a class="button gold" href="mailto:hello@kawan.org">Find a mentor <span>↗</span></a>
			</div>
		</div>
	</section>

	<section class="stories section-wrap" id="stories">
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

	<section class="cta-minimal">
		<div class="section-wrap">
			<div class="cta-content reveal">
				<h2>Ready?</h2>
				<a class="button gold large" href="mailto:hello@kawan.org">Get started <span>↗</span></a>
			</div>
		</div>
	</section>
</main>

<footer>
	<div class="footer-main section-wrap">
		<div class="footer-brand">
			<a class="brand inverse" href="#top">
				<span class="brand-mark" aria-hidden="true">
					<svg viewBox="0 0 44 44" fill="none">
						<path d="M5 27.5c7-12 16-15 33-12-7.5 2.8-11 8-12.2 15.2C20 24.8 13.2 24.5 5 27.5Z" fill="currentColor" />
						<path d="M10 32c8-5 15-5.8 24-3.2" stroke="currentColor" stroke-width="2.7" stroke-linecap="round" />
					</svg>
				</span>
				<span>Kawan</span>
			</a>
			<p>Guidance without borders.</p>
		</div>
		<div class="footer-links">
			<div><strong>LINKS</strong><a href="#programs">How we help</a><a href="#stories">Stories</a></div>
			<div><strong>GET INVOLVED</strong><a href="mailto:volunteer@kawan.org">Volunteer</a><a href="mailto:hello@kawan.org">Contact us</a></div>
		</div>
	</div>
	<div class="footer-bottom section-wrap">
		<span>© 2026 KAWAN.</span>
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

	.brand > span:last-child > span {
		color: var(--gold);
	}

	.brand-mark {
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
		gap: 18px;
		padding: 0 25px;
		border-radius: 999px;
		color: #fff;
		background: linear-gradient(135deg, var(--forest) 0%, #a08f86 100%);
		box-shadow: 0 12px 28px rgba(91, 74, 66, 0.13);
		font-size: 14px;
		font-weight: 700;
		transition: transform 0.2s ease, box-shadow 0.2s ease, filter 0.2s ease;
	}

	.button:hover {
		background: linear-gradient(135deg, var(--forest-dark) 0%, #927d71 100%);
		transform: translateY(-2px);
		box-shadow: 0 18px 32px rgba(91, 74, 66, 0.15);
		filter: saturate(1.05);
	}

	.button.small {
		min-height: 44px;
		padding: 0 19px;
	}

	.button.large {
		min-height: 60px;
		padding: 0 32px;
		font-size: 16px;
	}

	.button.gold {
		color: var(--ink);
		background: var(--gold);
		box-shadow: none;
	}

	.button.gold:hover {
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

	.welcome-to-text {
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
	.hero-shape {
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

	.about-intro {
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
	.mentor-section {
		padding: 120px 0;
		background: #ede4db;
	}

	.mentor-minimal {
		text-align: center;
		max-width: 600px;
		margin: 0 auto;
	}

	.mentor-dot {
		width: 80px;
		height: 80px;
		border: 2px solid var(--forest);
		border-radius: 50%;
		margin: 0 auto 40px;
	}

	.mentor-minimal h2 {
		font-size: 48px;
		margin: 0 0 16px 0;
		color: var(--ink);
		font-family: 'Playfair Display', serif;
		font-weight: 700;
		letter-spacing: -1px;
	}

	.mentor-minimal p {
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

		.hero-shape {
			display: none;
		}

		.about-content {
			grid-template-columns: 1fr;
			gap: 60px;
		}

		.about-content h2 {
			font-size: 32px;
		}

		.about-content h3 {
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

		.mentor-section {
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
</style>
