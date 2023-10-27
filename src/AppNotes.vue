<script setup lang="ts">
import { ref } from 'vue'

import ExForm from './components/forms/ExForm.vue'
import Box from './components/layout/Box.vue'
import AspectRatio from './components/layout/AsepectRatio.vue'
import Button from './components/forms/Button.vue'
import List from './components/data/List.vue'
import ListItem from './components/data/ListItem.vue'
import Text from './components/typo/Text.vue'
import Link from './components/Link.vue'
import Highlight from './components/typo/Highlight.vue'
import Table from './components/data/Table.vue'

const list = ref([
  { id: 1, name: 'Peter', url: 'https://tallpad.com/series/tailwind' },
  { id: 2, name: 'Hannes', url: 'https://tallpad.com/series/tailwind' },
  { id: 3, name: 'Karl', url: 'https://tallpad.com/series/tailwind' },
  { id: 4, name: 'Freddy', url: 'https://tallpad.com/series/tailwind' },
  { id: 5, name: 'Charly', url: 'https://tallpad.com/series/tailwind' }
])

const json = ref([])

const fetchJSON = () => {
  fetch('https://jsonplaceholder.typicode.com/users')
    .then((response) => response.json())
    .then((data) => (json.value = data))
}
</script>

<template>
  <Text
    >Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque
    laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto
    beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut
    odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt.
    Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit,
    sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam
    <Highlight code bold color="gray">
      aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam
      corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur?
    </Highlight>
    Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae
    consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur
  </Text>

  <Box name="3">
    <Box name="4">
      <Box h="300px" name="5"
        ><Box name="6"
          ><Box name="7">
            <Box name="8">
              <Box name="9"> <Box name="10"> </Box></Box> </Box
          ></Box>
        </Box>
      </Box>
    </Box>
  </Box>

  <Table
    :json="json"
    :table-headers="[
      { name: 'ID', key: 'id' },
      { name: 'Name', key: 'name' },
      { name: 'Email', key: 'email' },
      { name: 'Street', key: 'address.street' },
      { name: 'Suite', key: 'address.suite' },
      { name: 'Lat', key: 'address.geo.lat' },
      { name: 'Lng', key: 'address.geo.lng' }
    ]"
  />
  <Button @click="fetchJSON()">Fetch JSON</Button>

  <AspectRatio max-width="400px">
    <iframe
      src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3963.952912260219!2d3.375295414770757!3d6.5276316452784755!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x103b8b2ae68280c1%3A0xdc9e87a367c3d9cb!2sLagos!5e0!3m2!1sen!2sng!4v1567723392506!5m2!1sen!2sng"
    />
  </AspectRatio>

  <Box name="LetterBox" p="1rem" pt="1rem">
    <ExForm />
  </Box>

  <Box name="List">
    <List>
      <ListItem v-for="item in list" style="min-width: 100px; min-height: 50px">
        <Box name="Link" p="1rem">
          <Link href="https://tallpad.com/series/tailwind">Das ist ein Link</Link>
          <Text text-align="center" inline> {{ item.name }}</Text>
          <Button :href="item.url">Button</Button>
        </Box>
      </ListItem>
    </List>
  </Box>
</template>
