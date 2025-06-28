<script setup>
import { ref } from 'vue'

const message = ref('')

const fetchMessage = async () => {
  const res = await fetch('/api/hello')  // ya no necesita localhost:3000
  const data = await res.json()
  message.value = data.message
}
</script>
