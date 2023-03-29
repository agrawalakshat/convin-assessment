import React, { useState } from 'react';
import { Navbar, Nav, Container, Row, Col, Card, Button, Modal, Form } from 'react-bootstrap';

function App() {

  // State to manage buckets and cards
  const [buckets, setBuckets] = useState([
    {
      name: 'Entertainment Videos',
      cards: [
        {
          name: 'Card 1',
          link: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ'
        },
        {
          name: 'Card 2',
          link: 'https://www.youtube.com/watch?v=oHg5SJYRHA0'
        }
      ]
    },
    {
      name: 'Education Videos',
      cards: [
        {
          name: 'Card 3',
          link: 'https://www.youtube.com/watch?v=y8Kyi0WNg40'
        }
      ]
    }
  ]);

  // State to manage modal
  const [showModal, setShowModal] = useState(false);
  const [modalContent, setModalContent] = useState('');

  // State to manage new bucket/card form
  const [newBucketName, setNewBucketName] = useState('');
  const [newCardName, setNewCardName] = useState('');
  const [newCardLink, setNewCardLink] = useState('');
  const [selectedBucketIndex, setSelectedBucketIndex] = useState(0);

  // State to manage history
  const [history, setHistory] = useState([]);

  // Handler for showing modal
  const handleShowModal = (link) => {
    setModalContent(link);
    setShowModal(true);
  }

  // Handler for creating new bucket
  const handleCreateBucket = () => {
    const newBucket = {
      name: newBucketName,
      cards: []
    };
    setBuckets([...buckets, newBucket]);
    setNewBucketName('');
  }

  // Handler for creating new card
  const handleCreateCard = () => {
    const newCard = {
      name: newCardName,
      link: newCardLink
    };
    const updatedBuckets = [...buckets];
    updatedBuckets[selectedBucketIndex].cards.push(newCard);
    setBuckets(updatedBuckets);
    setNewCardName('');
    setNewCardLink('');
  }

  // Handler for deleting a card
  const handleDeleteCard = (bucketIndex, cardIndex) => {
    const updatedBuckets = [...buckets];
    updatedBuckets[bucketIndex].cards.splice(cardIndex, 1);
    setBuckets(updatedBuckets);
  }

  // Handler for deleting multiple cards
  const handleDeleteMultipleCards = (bucketIndex, selectedCardIndexes) => {
    const updatedBuckets = [...buckets];
    const cardsToKeep = updatedBuckets[bucketIndex].cards.filter((card, index) => !selectedCardIndexes.includes(index));
    updatedBuckets[bucketIndex].cards = cardsToKeep;
    setBuckets(updatedBuckets);
  }

  // Handler for moving a card to another bucket
  const handleMoveCard = (sourceBucketIndex, targetBucketIndex, cardIndex) => {
    const updatedBuckets = [...buckets];
    const cardToMove = updatedBuckets[sourceBucketIndex].cards[cardIndex];
    updatedBuckets[sourceBucketIndex].cards.splice(cardIndex, 1);
    updatedBuckets[targetBucketIndex].cards.push(cardToMove);
    setBuckets(updatedBuckets);
  }

  // Handler
