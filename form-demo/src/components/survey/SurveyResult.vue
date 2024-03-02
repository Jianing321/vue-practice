<template>
	<li>
		<p>
			The Supervisor Name:
			<span class="highlight">{{ name }}</span>
			The Project:
			<span class="highlight">{{ project }}</span>
			University:
			<span class="highlight">{{ university }}</span>
			Supervisor Email:
			<span class="highlight" @click="sendEmail(email)">{{ email }}</span>
			rated the learning experience
			<span :class="ratingClass">{{ rating }}</span>.
		</p>
	</li>
</template>

<script>
export default {
	props: ['name', 'project', 'university', 'email', 'rating'],
	computed: {
		ratingClass() {
			return 'highlight rating--' + this.rating;
		},
	},
	methods: {
		sendEmail(email) {
			const subject = '邮件主题';
			const body = '邮件正文';

			const mailtoLink = `mailto:${email}?subject=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;

			// 打开默认的邮件客户端
			window.location.href = mailtoLink;
		}
	}
};
</script>

<style scoped>
li {
	margin: 1rem 0;
	border: 1px solid #ccc;
	padding: 1rem;
}

h3,
p {
	font-size: 1rem;
	margin: 0.5rem 0;
}

.highlight {
	font-weight: bold;
}

.rating--poor {
	color: #b80056;
}

.rating--average {
	color: #330075;
}

.rating--great {
	color: #008327;
}
</style>